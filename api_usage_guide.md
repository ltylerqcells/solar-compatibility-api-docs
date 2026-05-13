# Solar Compatibility API — Usage Guide

Internal documentation — Qcells SQT
May 2026

---

## Table of Contents

1. [Overview](#1-overview)
2. [Authentication and Setup](#2-authentication-and-setup)
3. [The Combined Endpoint](#3-the-combined-endpoint)
4. [Request Structure](#4-request-structure)
5. [Response Structure](#5-response-structure)
6. [Field Reference](#6-field-reference)
7. [Issue Messages](#7-issue-messages)
8. [Common Patterns and Examples](#8-common-patterns-and-examples)
9. [How Period and Calculation Logic Work](#9-how-period-and-calculation-logic-work)
10. [Error Handling and HTTP Status Codes](#10-error-handling-and-http-status-codes)
11. [Limitations and Known Issues](#11-limitations-and-known-issues)

---

## 1. Overview

The Solar Compatibility API is an internal service that validates a solar installation's bill of materials (BOM) against three sets of rules:

- **Structural compatibility** — modules, inverters, batteries, and accessories must form a valid system
- **UL 2703 mechanical certification** — racking SKUs must share a UL 2703 cross-listed System Family with a single anchor maker
- **Domestic Content Adder (DCA)** — eligibility for the federal tax credit under IRS Notice 2024-41 / 2025-08
- **Foreign Entity of Concern (FEOC)** — restrictions on prohibited-source content (active 2026 onward)

Given a list of equipment SKUs and an installation date, the API returns whether the install qualifies, what percentage of domestic content was achieved, and what (if anything) needs to change.

### What this guide covers

This guide focuses on the primary endpoint: `POST /v1/check/combined`. Most callers should use only this endpoint. It runs the full pipeline in one call and returns a unified result.

Standalone endpoints (`/v1/check/dca`, `/v1/check/feoc`, `/v1/check/ul2703`, `/v1/validate`) exist for specialized use cases but are out of scope for this guide.

### What gets checked

| Check | Source of truth | When it fails |
|---|---|---|
| Equipment validity | Airtable AVL tables | SKU not found in PVAVL/IAVL/BAVL/MSAVL |
| Structural compatibility | `app/compatibility.py` | AC module + non-Q.MI inverter, mismatched BatteryA/BatteryB OEM, etc. |
| UL 2703 | MSAVL Maker / System Family / Crosslisting fields | Racking spans multiple makers without a cross-listing chain |
| DCA percentage | AVL DCA% fields, applied per IRS formula | Below threshold for the period (results in WARNING, not FAIL) |
| FEOC percentage | AVL FEOC% fields | Below threshold for the period (results in WARNING, not FAIL) |

### Key concepts

- **Tax period**: derived from the installation date. Determines which DCA/FEOC thresholds apply and which formula is used.
- **System type**: "MLPE" (microinverter or module-level power electronics) or "String" (string inverter). Resolved from the inverter's IAVL record.
- **Variant SKU**: the API automatically swaps base SKUs to DCA-eligible variant SKUs (e.g., `Q.PEAK DUO BLK ML-G10+ 410` → `DCA.17 Q.PEAK DUO BLK ML-G10+ 410`) based on material codes and serial numbers provided.

---

## 2. Authentication and Setup

### Base URLs

| Environment | URL |
|---|---|
| Production | `https://solar-compatibility-api.onrender.com` |
| Local development | `http://localhost:8000` |

### Authentication

All endpoints require an API key passed via the `X-API-Key` header. Keys are managed by the SQT team. Reach out for a key if you don't have one.

```http
X-API-Key: <your-api-key>
Content-Type: application/json
```

### Health check

To verify the service is reachable and your key works:

```http
GET /v1/health
```

Returns `200 OK` with a JSON body indicating service status. No authentication required.

### Sample minimal request

```bash
curl -X POST https://solar-compatibility-api.onrender.com/v1/check/combined \
  -H "X-API-Key: $API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "installation-date": "2026-06-15",
    "bom": {
      "pv": [{"sku": "Q.PEAK DUO BLK ML-G10+ 410"}],
      "inverter": [{"sku": "USE7600H-USMNBL75"}]
    },
    "other equipment": {
      "Rail": ["XR-10-168M-US"],
      "Mid Clamp": ["XR-MID-01-B1-US"],
      "End Clamp": ["UFO-END-01-B1-US"],
      "Roof Flashing/Mount/Clamp": ["QMTR-BM-A-12"]
    }
  }'
```

---

## 3. The Combined Endpoint

```http
POST /v1/check/combined
```

This is the primary endpoint. A single request submits the entire BOM; a single response returns the full validation result.

### Request flow

The endpoint runs the following pipeline. If any step produces a `FAIL`-prefixed issue, the pipeline short-circuits and returns `valid: false`.

1. **Preflight validation** — required SKUs are present, no multi-SKU constraints are violated, identifiers are not duplicated between per-item and pooled
2. **SKU variant resolution** — base SKUs are swapped to DCA-eligible or DCA-ineligible variant SKUs based on material codes and serial numbers
3. **AVL fetch** — Airtable records are fetched for every SKU
4. **Validation** — each SKU's record is verified to exist in the right table and have the right subcategory
5. **Battery role inference** — batteries are assigned roles (BatteryA, BatteryB, BatteryExpansion) from their BAVL records
6. **Q.MI module-inverter pairing** — if the inverter is `Q.MI.349B-G1` and the module is in the Q.TRON BLK M-G2+/AC family, the inverter SKU is auto-swapped to the paired variant
7. **Compatibility** — module/inverter/battery structural rules are enforced
8. **UL 2703** — racking SKUs are checked for cross-listed compatibility
9. **DCA** — domestic content percentages are computed per side
10. **FEOC** — foreign-entity-of-concern percentages are computed per side
11. **Response assembly** — results are returned in a unified structure

### Response semantics

The response is always returned with HTTP 200, regardless of whether the BOM passed validation. Use the `valid` field, `pass_*` flags, and `issues` array to determine the outcome.

The exception is shape errors (malformed JSON, missing required fields at the schema level): these return HTTP 422.

---

## 4. Request Structure

### Top-level shape

```json
{
  "installation-date": "2026-06-15",
  "bom": { ... },
  "other equipment": { ... }
}
```

| Field | Required | Type | Description |
|---|---|---|---|
| `installation-date` | **Required** | date string (ISO 8601) | The system's installation date. Determines the tax period. Format: `"YYYY-MM-DD"` or `"YYYY-MM-DDTHH:MM:SS"` (time portion ignored). |
| `bom` | **Required** | object | Bill of Materials. See section 4.1. |
| `other equipment` | **Required** | object | Racking and accessory SKUs. See section 4.2. |

### 4.1 BOM Structure

The `bom` object holds three required arrays — `pv`, `inverter`, `battery` — and four optional pooled-identifier arrays.

```json
{
  "pv": [
    {
      "sku": "Q.PEAK DUO BLK ML-G10+ 410",
      "serial_numbers": ["SN1", "SN2"],
      "material_codes": ["MC123"],
      "quantity": 17
    }
  ],
  "inverter": [
    {"sku": "USE7600H-USMNBL75", "serial_numbers": []}
  ],
  "battery": [
    {"sku": "1707000-21-y", "serial_numbers": []}
  ],
  "pv_serial_numbers": [],
  "pv_material_codes": [],
  "inverter_serial_numbers": [],
  "battery_serial_numbers": []
}
```

#### BomItem (each entry in `pv`, `inverter`, `battery`)

| Field | Required | Type | Default | Notes |
|---|---|---|---|---|
| `sku` | **Required** | string | — | Base SKU. The API resolves to variants automatically. |
| `serial_numbers` | Optional | array of strings | `[]` | Per-item alternative to pooled. |
| `material_codes` | Optional | array of strings | `[]` | PV only. Ignored for inverter/battery. |
| `quantity` | **Required on all battery items; required on PV items when batteries are present** | integer | `null` | Battery count for battery items (used in capacity-weighted DCA/FEOC averages). Module count for PV items (used for the 2024 IRS unified formula). |

#### `pv` array constraints

- **Must have at least one item.** Empty `pv` array → `FAIL: Module SKU is required`.
- **All items must share one SKU.** Multiple distinct SKUs → `FAIL: Multiple Module SKUs not allowed`. Multiple items with the SAME SKU are allowed (treated as one module type with summed quantities).
- **`quantity` is required if batteries are present.** Without it for 2024 cases, the unified DCA formula cannot be computed.

#### `inverter` array constraints

- **Must have at least one item.** Empty array → `FAIL: Inverter SKU is required`.
- **All items must share one SKU.** Multiple distinct inverter SKUs → `FAIL: Multiple inverter SKUs require manual review`. The system does not currently support automatic processing of mixed-inverter installs; these are flagged for manual review.

#### `battery` array constraints

- **Optional.** Defaults to empty.
- **Maximum 3 items.** More than 3 → `FAIL: At most 3 batteries allowed, got <N>`.
- **`quantity` required on every battery item.** Missing → `FAIL: Battery SKU '<sku>' requires a quantity`. Quantity is used in capacity-weighted DCA and FEOC averages.
- **Different SKUs allowed.** Battery roles (BatteryA, BatteryB, BatteryExpansion) are inferred from BAVL records.

#### Identifier rules (serial_numbers, material_codes)

Identifiers can be specified per-item OR pooled at the category level, but not both for the same category. Mixing → `FAIL: Cannot specify both per-item and pooled <type> for <category>`.

- **Per-item**: each BomItem has its own `serial_numbers` / `material_codes` arrays.
- **Pooled**: the `bom` object has `pv_serial_numbers` / `pv_material_codes` / `inverter_serial_numbers` / `battery_serial_numbers`. These apply to all items in that category.

For multi-item PV BOMs (multiple BomItems with the same SKU but split across shipments), all per-item identifiers are flattened together before resolution. So if item 1 has SNs `["A", "B"]` and item 2 has `["C"]`, the resolver sees `["A", "B", "C"]`.

### 4.2 Other Equipment

The `other equipment` object holds racking and accessory SKUs. Required buckets must be present; optional buckets can be omitted.

```json
{
  "Rail": ["XR-10-168M-US"],
  "Mid Clamp": ["XR-MID-01-B1-US"],
  "End Clamp": ["UFO-END-01-B1-US"],
  "Splice": ["XR10-BOSS-01-M1-US"],
  "MLPE Mount": ["BHW-MI-01-A1-US"],
  "Roof Flashing/Mount/Clamp": ["QMTR-BM-A-12"],
  "L-foot / Standoff / Tilt-leg": ["LFT-03-M1"],
  "Accessories": ["XR-10-CAP01-B1"],
  "MLPE/Optimizer": "U650-1GM4MRMU",
  "Gateway": "ENV-S-EM-230"
}
```

| Field | Required | Type | Notes |
|---|---|---|---|
| `Rail` | **Required** | array | At least one rail SKU. Multiple rails allowed up to a configured maximum. |
| `Mid Clamp` | **Required** | array | At least one mid clamp SKU. |
| `End Clamp` | **Required** | array | At least one end clamp SKU. |
| `Roof Flashing/Mount/Clamp` | **One-of (with L-foot)** | array | At least one of this OR `L-foot / Standoff / Tilt-leg` is required. |
| `L-foot / Standoff / Tilt-leg` | **One-of (with Roof Flashing)** | array | See above. |
| `Splice` | Optional | array | |
| `MLPE Mount` | Optional | array | |
| `Accessories` | Optional | array | |
| `MLPE/Optimizer` | Optional | single string | Single SKU, not an array. |
| `Gateway` | Optional | single string | Single SKU, not an array. |

---

## 5. Response Structure

The response is a single JSON object with five sections: top-level status, DCA results, FEOC results, components breakdown, and issues.

```json
{
  "valid": true,
  "system_type": "MLPE",

  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": 0.595,
  "unified_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,

  "pass_feoc_pv": true,
  "pass_feoc_ess": true,
  "pv_side_total_feoc": 0.617,
  "ess_side_total_feoc": 0.568,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,

  "components": [...],
  "issues": [...]
}
```

### 5.1 Top-level fields

| Field | Type | Description |
|---|---|---|
| `valid` | bool | `true` if the request was processable end-to-end. `false` if any preflight, validation, compatibility, or UL 2703 step produced a `FAIL`. |
| `system_type` | string \| null | `"MLPE"`, `"String"`, or `null` if unresolved. |

### 5.2 DCA fields

| Field | Type | Description |
|---|---|---|
| `pass_dca_pv` | bool \| null | Whether PV-side DCA met the threshold. `null` if not computable. |
| `pass_dca_ess` | bool \| null | Whether ESS-side DCA met the threshold. `null` if no batteries or not computable. |
| `pv_side_total_dca` | float \| null | PV-side DCA fraction (0.0–1.0+). |
| `ess_side_total_dca` | float \| null | ESS-side DCA fraction. `null` if no batteries. |
| `unified_total_dca` | float \| null | **2024 only.** Result of the IRS unified formula. `null` for 2025+. |
| `dca_pv_threshold` | float | The threshold that was applied. |
| `dca_ess_threshold` | float | The threshold that was applied. |

### 5.3 FEOC fields

| Field | Type | Description |
|---|---|---|
| `pass_feoc_pv` | bool \| null | Whether PV-side FEOC met the threshold. `null` if FEOC inactive (pre-2026) or not computable. |
| `pass_feoc_ess` | bool \| null | Whether ESS-side FEOC met the threshold. `null` (no batteries or not computable). |
| `pv_side_total_feoc` | float \| null | PV-side FEOC fraction. `null` if FEOC inactive. |
| `ess_side_total_feoc` | float \| null | ESS-side FEOC fraction. `null` if FEOC inactive or no batteries. |
| `feoc_pv_threshold` | float \| null | The threshold that was applied. `null` for pre-2026. |
| `feoc_ess_threshold` | float \| null | The threshold that was applied. `null` for pre-2026. |

### 5.4 Components

The `components` array breaks down per-component contributions to the totals. There is one entry per logical component: Module, Inverter, Racking, ESS (if present).

```json
{
  "key": "Racking",
  "sku": null,
  "skus": ["XR-10-168M-US", "XR-MID-01-B1-US", "UFO-END-01-B1-US"],
  "dca_pct": 0.227,
  "feoc_pct": null,
  "notes": [
    "Rail (XR-10-168M-US): 18.70%",
    "Mid Clamp (XR-MID-01-B1-US): 11.10%",
    "End Clamp (UFO-END-01-B1-US): 11.10%"
  ]
}
```

| Field | Type | Description |
|---|---|---|
| `key` | string | `"Module"`, `"Inverter"`, `"Racking"`, or `"ESS"`. |
| `sku` | string \| null | Set for single-SKU components (Module, Inverter). `null` for multi-SKU. |
| `skus` | array \| null | Set for multi-SKU components (Racking, ESS). `null` for single-SKU. |
| `dca_pct` | float \| null | Per-component DCA contribution. |
| `feoc_pct` | float \| null | Per-component FEOC contribution. Always `null` for Racking (FEOC excludes racking). |
| `notes` | array of strings | Per-SKU breakdown for multi-SKU components; empty for single-SKU. |

### 5.5 Issues

The `issues` array contains all messages emitted during processing. Each message has a prefix:

- **`FAIL:`** — critical, request was not processable. Response will have `valid: false` and most math fields `null`.
- **`WARNING:`** — non-fatal data issue, math continues. Includes threshold misses (e.g., DCA below 50% for 2026).
- **`NOTE:`** — informational, often explaining decisions made (e.g., Q.MI variant swap).

A request can produce zero, one, or many issues. Frontend code should iterate the array and display by prefix or filter as needed.

See [section 7](#7-issue-messages) for a full catalog.

---

## 6. Field Reference

### 6.1 When fields go null

The most common scenarios for null math fields:

| Scenario | Effect |
|---|---|
| Preflight FAIL | All math fields null, `valid: false`, components empty |
| Validation FAIL (SKU not in AVL) | Same as preflight FAIL |
| Compatibility FAIL | Same |
| UL 2703 FAIL | Same |
| Multi-inverter (different SKUs) | FAIL with manual-review message; same as preflight FAIL |
| DCA computed, no battery | `ess_side_total_dca`, `pass_dca_ess` null; `unified_total_dca` null for 2026+ but populated for 2024 |
| 2024 unified couldn't compute (missing PV size or system_type) | `unified_total_dca` null, `pass_dca_pv` and `pass_dca_ess` set to false |
| FEOC inactive era (pre-2026) | All FEOC fields null, `pass_feoc_pv` null, `pass_feoc_ess` null |
| System type unresolved | All DCA/FEOC computations fail or return null |

### 6.2 Threshold reference

| Period | DCA PV | DCA ESS | FEOC PV | FEOC ESS |
|---|---|---|---|---|
| 2024 | 40% (unified) | 40% (unified) | — | — |
| 2025-Q1 | 40% | 40% | — | — |
| 2025-Q2 | 40% | 40% | — | — |
| 2025-Q3 | 45% | 45% | — | — |
| 2026 | 50% | 50% | 40% | 55% |
| 2027 | 55% | 55% | 45% | 60% |
| 2028 | 55% | 55% | 50% | 65% |

**FEOC thresholds**: a threshold is the *minimum* domestic-content percentage required (DCA) or the *minimum* permitted-source percentage required (FEOC). Below threshold → fails the test for that side.

### 6.3 Combination percentages

The DCA racking calculation includes a "combination bonus" added when both rails AND fasteners are DCA-eligible. The bonus depends on the period and system type:

| Period | MLPE | String |
|---|---|---|
| 2024 | 6.1% | 8.7% |
| 2025+ | 1.1% | 1.4% |

### 6.4 IRS unified formula (2024 only)

For 2024 installs with batteries present, DCA is computed using:

```
unified_total = (PV_size × PV_DCA + multiplier × BESS_size × BESS_DCA)
                / (PV_size + multiplier × BESS_size)
```

Where:
- `PV_size` (kW) = total module quantity × wattage / 1000
- `PV_DCA` = module + inverter + racking_production
- `multiplier` = 0.99 (String) or 0.69 (MLPE)
- `BESS_size` (kWh) = sum of battery quantity × capacity
- `BESS_DCA` = capacity-weighted average of battery DCA percentages

**Pass condition**: `unified_total >= 0.40`

For 2024 installs **without** batteries, `unified_total = pv_portion` (just module + inverter + racking_production). No ratio.

---

## 7. Issue Messages

This section catalogs every issue message the API can emit, organized by stage and prefix.

### 7.1 Preflight FAILs

Module / inverter / battery requirements:

- `FAIL: Module SKU is required`
- `FAIL: Multiple Module SKUs not allowed (<sku1>, <sku2>, ...)`
- `FAIL: Module SKU '<sku>' requires a quantity when batteries are in the BOM (needed for 2024 unified DCA calculation)`
- `FAIL: Inverter SKU is required`
- `FAIL: Multiple inverter SKUs require manual review`
- `FAIL: At most 3 batteries allowed, got <N>`

Racking / equipment requirements:

- `FAIL: Multiple <bucket> SKUs not allowed (<sku1>, <sku2>, ...)` — for buckets that allow only one SKU
- `FAIL: At most <N> distinct Rail SKUs allowed, got <N> (<skus>)`
- `FAIL: Missing required product type: <key>`
- `FAIL: Must include either Roof Flashing/Mount/Clamp or L-foot / Standoff / Tilt-leg (at least one required)`

Identifier shape:

- `FAIL: Cannot specify both per-item and pooled serial_numbers for <category>. Use one or the other.`
- `FAIL: Cannot specify both per-item and pooled material_codes for <category>. Use one or the other.`

Battery role inference:

- `FAIL: Expansion battery requires a non-expansion base unit`
- `FAIL: At least one non-expansion battery required`
- `FAIL: Three non-expansion batteries is not a supported configuration`
- `FAIL: <N> batteries is not supported`
- `FAIL: BatteryA is required when BatteryB or BatteryExpansion is provided`

### 7.2 SKU resolver issues

The resolver swaps base SKUs to DCA-eligible variant SKUs based on identifiers. Behavior is permissive for modules (Q.PEAK family) and strict for batteries/IQ8 inverters.

**Module resolver (Q.PEAK material code / SN range) — permissive:**

- `WARNING: <help_text>. No material code provided; defaulting to non-DCA variant.`
- `WARNING: <help_text>. Inconsistent material codes for '<sku>'; defaulting to non-DCA variant.`
- `WARNING: <help_text>. No serial number provided; defaulting to non-DCA variant.`
- `WARNING: <help_text>. Inconsistent serial numbers for '<sku>'; defaulting to non-DCA variant.`

**Non-module resolver (batteries, IQ8 inverters) — strict:**

- `FAIL: <help_text>. Serial number required to determine variant — none provided.`
- `FAIL: <help_text>. Serial number '<sn>' does not match any known pattern for '<sku>'. No equivalent product exists in AVL for this serial number.`
- `FAIL: <help_text>. Inconsistent serial numbers for '<sku>'. Provided SNs resolve to different variants: <list>.`

The strictness difference is by design: Q.PEAK SKUs have a "non-DCA fallback" record in PVAVL, so missing identifiers can fall back gracefully. IQ8 inverters and IQBATTERY-5P-1P-NA-DOM have no such fallback — every variant is keyed on a specific SN range — so missing/unmatched SNs result in a hard FAIL.

**Identifier irrelevance warnings:**

- `WARNING: Ignoring serial numbers for '<sku>' — this SKU uses material code for DCA/FEOC determination`
- `WARNING: Ignoring material code for '<sku>' — this SKU uses serial number for DCA/FEOC determination`
- `WARNING: Ignoring serial numbers for '<sku>' — no DCA/FEOC rule applies to this SKU`
- `WARNING: Ignoring material code for '<sku>' — no DCA/FEOC rule applies to this SKU`

### 7.3 Q.MI module-inverter pairing

- `NOTE: Inverter '<bare>' resolved to '<variant>' because module is '<trimmed_name>'`
- `FAIL: '<target>' not found in IAVL after Q.MI variant resolution`
- `FAIL: Inverter '<variant>' is specifically for Q.TRON BLK M-G2+/AC modules. Submitted module is '<trimmed_name>'. Use '<bare>' for this module.`

### 7.4 Validation issues

- `FAIL: Unknown product type(s): <types>`
- `FAIL: <key> SKU '<sku>' not found in MSAVL`
- `FAIL: <key> SKU '<sku>' not found in <table>`
- `FAIL: <key> SKU '<sku>' is not valid for this product type. Expected: <expected>. Found: <found>`
- `WARNING: <key> SKU '<sku>' has multiple subcategories filled (<list>) — data issue in MSAVL`

### 7.5 Compatibility FAILs

Module ↔ Inverter:

- `FAIL: AC modules are only compatible with Q.MI-series inverters (inverter series is '<inv_series>')`
- `FAIL: DC modules are not compatible with Q.MI-series inverters`
- `WARNING: Module has unrecognised module_type '<type>' — cannot check module/inverter compatibility`

Inverter ↔ MLPE/Optimizer:

- `FAIL: MLPE/Optimizer is required for <inv_oem> MLPE inverters`
- `FAIL: MLPE Mount is required for MLPE/microinverter systems`
- `FAIL: MLPE/Optimizer must be same OEM as Inverter`

Inverter ↔ Gateway:

- `FAIL: Gateway must be same OEM as Inverter (or ConnectDER); Gateway OEM is '<gw_oem>'`

Batteries:

- `FAIL: BatteryA must not be an expansion unit`
- `FAIL: BatteryB must be same OEM as BatteryA`
- `FAIL: BatteryB must be same model as BatteryA`
- `FAIL: BatteryB must not be an expansion unit`
- `FAIL: BatteryExpansion must be an expansion unit`
- `FAIL: BatteryExpansion must be same OEM as BatteryA`
- `FAIL: BatteryExpansion requires a BatteryA to be present`

### 7.6 UL 2703

- `FAIL: No equipment provided`
- `FAIL: <candidate> items have no shared System Family (<skus>)`
- `FAIL: <candidate> cannot be anchor — missing from Crosslisting of: <missing>`

### 7.7 DCA messages

System type resolution:

- `FAIL: Inverter is required for DCA check`
- `WARNING: Inverter has blank or unrecognised Inverter Type '<type>' — data issue in IAVL`

Missing data warnings (only when the SKU is on DCA AVL):

- `WARNING: Module '<sku>' is on DCA AVL but has no <year> <system_type> DCA % — data issue in PVAVL`
- `WARNING: Inverter '<sku>' is on DCA AVL but has no <year> <system_type> DCA % — data issue in IAVL`
- `WARNING: Rail '<sku>' is on DCA AVL but has no <year> <system_type> DCA % — data issue in MSAVL`
- `WARNING: Fastener '<sku>' (<key>) is on DCA AVL but has no <year> <system_type> DCA % — data issue in MSAVL`
- `WARNING: Battery '<sku>' (<key>) is on DCA AVL but has no <year> <system_type> DCA % — data issue in BAVL`

2024 unified-specific:

- `WARNING: Module '<sku>' has no wattage — PV size cannot be computed for 2024 unified DCA`
- `WARNING: Module '<sku>' has unparseable wattage '<value>' — PV size cannot be computed`
- `FAIL: PV Size could not be computed. Therefore, DCA% could not be computed.`
- `NOTE: 2024 uses unified DCA check — combined PV+ESS sum (<X>%) compared to threshold (<Y>%)`

Battery data:

- `WARNING: Battery SKU '<sku>' (<key>) not found — excluded from weighted average`
- `WARNING: Battery '<sku>' has no capacity value — excluded from weighted average`
- `WARNING: Battery '<sku>' has non-numeric capacity '<value>' — excluded`

Racking:

- `WARNING: Rails contribute 0 to DCA — not all rails are DCA eligible`
- `WARNING: Fasteners contribute 0 to DCA — not all fasteners are DCA eligible`

Threshold misses (downgraded from FAIL to WARNING — install is processable, just doesn't qualify):

- `WARNING: PV-side DCA <X>% below threshold <Y>%`
- `WARNING: ESS-side DCA <X>% below threshold <Y>%`
- `WARNING: Combined DCA <X>% below 2024 unified threshold <Y>%`

### 7.8 FEOC messages

- `WARNING: Battery '<sku>' has no capacity — excluded from FEOC weighted average`
- `WARNING: Battery '<sku>' has non-numeric capacity '<value>' — excluded`
- `NOTE: ESS-side FEOC cannot be computed — system type unresolved`
- `WARNING: PV-side FEOC <X>% below threshold <Y>%`
- `WARNING: ESS-side FEOC <X>% below threshold <Y>%`

---

## 8. Common Patterns and Examples

### 8.1 Minimum viable request (no battery, 2026)

```json
{
  "installation-date": "2026-08-15",
  "bom": {
    "pv": [{"sku": "Q.PEAK DUO BLK ML-G10+ 410"}],
    "inverter": [{"sku": "USE7600H-USMNBL75"}]
  },
  "other equipment": {
    "Rail": ["XR-10-168M-US"],
    "Mid Clamp": ["XR-MID-01-B1-US"],
    "End Clamp": ["UFO-END-01-B1-US"],
    "Roof Flashing/Mount/Clamp": ["QMTR-BM-A-12"]
  }
}
```

### 8.2 Full request with battery and identifiers (2026)

```json
{
  "installation-date": "2026-06-15",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+ 410",
        "material_codes": ["MC4017"],
        "quantity": 17
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US",
        "serial_numbers": ["542600100001"]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM",
        "serial_numbers": ["542600200001"],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "Rail": ["XR-10-168M-US"],
    "Mid Clamp": ["XR-MID-01-B1-US"],
    "End Clamp": ["UFO-END-01-B1-US"],
    "Splice": ["XR10-BOSS-01-M1-US"],
    "MLPE Mount": ["BHW-MI-01-A1-US"],
    "Roof Flashing/Mount/Clamp": ["QMTR-BM-A-12"],
    "Accessories": ["XR-10-CAP01-B1"]
  }
}
```

### 8.3 2024 install with battery (requires `quantity`)

```json
{
  "installation-date": "2024-09-15",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 410",
        "quantity": 20
      }
    ],
    "inverter": [
      {"sku": "USE5700H-USMNBE78"}
    ],
    "battery": [
      {"sku": "UBAT-10K1PS0B-03",
      "quantity": 1
      }
    ]
  },
  "other equipment": {
    "Rail": ["232-10095-USA"],
    "Mid Clamp": ["242-02071-USA"],
    "End Clamp": ["242-02073-USA"],
    "Splice": ["242-01213-USA"],
    "MLPE Mount": ["242-10034-USA"],
    "Roof Flashing/Mount/Clamp": ["242-02729"]
  }
}
```

For 2024, the response will include a populated `unified_total_dca` field and the threshold check uses the unified value rather than separate PV/ESS thresholds.

### 8.4 Pooled identifiers

If serial numbers apply to all PV items rather than being per-item, use pooled fields:

```json
{
  "bom": {
    "pv": [
      {"sku": "Q.PEAK DUO BLK ML-G10+ 410", "quantity": 10},
      {"sku": "Q.PEAK DUO BLK ML-G10+ 410", "quantity": 7}
    ],
    "pv_serial_numbers": ["SN1", "SN2", "SN3"],
    "pv_material_codes": ["MC4017"],
    "inverter": [{"sku": "USE7600H-USMNBL75"}]
  }
}
```

The pooled identifiers apply to ALL items in that category. Mix per-item and pooled in the same category → `FAIL`.

### 8.5 Sample response (2026, fully passing)

```json
{
  "valid": true,
  "system_type": "MLPE",
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": 0.595,
  "unified_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "pass_feoc_pv": true,
  "pass_feoc_ess": true,
  "pv_side_total_feoc": 0.617,
  "ess_side_total_feoc": 0.568,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "components": [
    {
      "key": "Module",
      "sku": "DCA.17 Q.PEAK DUO BLK ML-G10+ 410",
      "skus": null,
      "dca_pct": 0.039,
      "feoc_pct": 0.311,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE11400H-USSKBEZ8 (11400W)",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": ["XR-10-168M-US", "XR-MID-01-B1-US", "UFO-END-01-B1-US"],
      "dca_pct": 0.227,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 18.70%",
        "Mid Clamp (XR-MID-01-B1-US): 11.10%",
        "End Clamp (UFO-END-01-B1-US): 11.10%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": ["1707000-21-y"],
      "dca_pct": 0.595,
      "feoc_pct": 0.568,
      "notes": ["BatteryA (1707000-21-y): qty=1, capacity=13.5 kWh"]
    }
  ],
  "issues": []
}
```

### 8.6 Sample response (2026, threshold miss)

```json
{
  "valid": true,
  "system_type": "MLPE",
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.398,
  "ess_side_total_dca": null,
  "unified_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "pass_feoc_pv": false,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": 0.311,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "components": [...],
  "issues": [
    "WARNING: PV-side DCA 39.8% below threshold 50%",
    "WARNING: PV-side FEOC 31.1% below threshold 40%"
  ]
}
```

Note that `valid` is still `true` — the install was successfully validated; it just doesn't meet the DCA/FEOC thresholds. The pass flags reflect the threshold check.

### 8.7 Sample response (preflight FAIL)

```json
{
  "valid": false,
  "system_type": null,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "unified_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "components": [],
  "issues": [
    "FAIL: Multiple Module SKUs not allowed (Q.PEAK DUO BLK ML-G10+ 420, DCA.17 Q.PEAK DUO BLK ML-G10+ 420)"
  ]
}
```

When `valid` is `false`, all math fields are `null`, components is empty, and the issues array explains why.

---

## 9. How Period and Calculation Logic Work

### 9.1 Period from date

The installation date determines the tax period:

| Date range | Period | DCA fields read from |
|---|---|---|
| 2024-01-01 to 2024-12-31 | 2024 | 2024 column |
| 2025-01-01 to 2025-04-15 | 2025-Q1 | **2024 column** (per Notice 08 clarification) |
| 2025-04-16 to 2025-06-15 | 2025-Q2 | 2025 column |
| 2025-06-16 to 2025-12-31 | 2025-Q3 | 2025 column |
| 2026 | 2026 | 2025 column |
| 2027 | 2027 | 2025 column |
| 2028 | 2028 | 2025 column |

**2025-Q1 quirk**: DCA percentages read from the 2024 column because IRS Notice 08 specifies the 2024 values continue through Q1. However, the calculation logic uses the 2025+ formula (separate PV/ESS thresholds), not the 2024 unified formula.

### 9.2 DCA calculation logic by era

**2024 (Jan-Dec 2024 installs):**

If batteries present:
```
unified_total = (PV_size × PV_DCA + multiplier × BESS_size × BESS_DCA)
                / (PV_size + multiplier × BESS_size)
```

If no batteries:
```
unified_total = PV_DCA  (just module + inverter + racking_production)
```

Pass condition: `unified_total >= 0.40`. The `unified_total_dca` field in the response holds this value.

**2025-Q1 onward:**

```
PV-side check:    pv_side_total_dca >= dca_pv_threshold
ESS-side check:   ess_side_total_dca >= dca_ess_threshold  (when batteries present)
```

Each side checked independently. The `unified_total_dca` field is `null`.

### 9.3 PV-side DCA composition

```
PV-side total = module_dca + inverter_dca + racking_production
```

Where:

```
racking_production = combination_pct + max(rail_pcts) + max(fastener_pcts)
```

Each piece can independently contribute or not:
- If ALL rails in the BOM are DCA-eligible → `max(rail_pcts)` contributes
- If ANY rail is non-DCA → rails contribute 0 (and a `WARNING` is added)
- Same logic for fasteners
- `combination_pct` only applies when BOTH rails AND fasteners are fully DCA-eligible

### 9.4 ESS-side DCA composition

Capacity-weighted average across batteries:

```
ess_side_total = Σ (battery_dca × capacity × quantity) / Σ (capacity × quantity)
```

A battery with no DCA% contributes 0 (its capacity stays in the denominator, pulling the average down).

### 9.5 FEOC composition

PV-side FEOC:
```
pv_side_total_feoc = module_feoc + inverter_feoc
```
(No racking; FEOC excludes racking by IRS spec.)

ESS-side FEOC: capacity-weighted average, identical structure to ESS DCA.

### 9.6 SKU variant resolution

The API resolves base SKUs to DCA-eligible variants based on identifiers provided. Customers send the base SKU (e.g., `Q.PEAK DUO BLK ML-G10+ 410`). The API returns whichever variant the identifiers indicate.

| Family | Identifier checked | Resolution behavior |
|---|---|---|
| Q.PEAK modules | Material code | Permissive — missing/wrong code → base SKU (non-DCA fallback) + WARNING |
| Q.PEAK modules | Serial number range | Permissive — same as above |
| IQBATTERY-5P-1P-NA | Serial number prefix (54 vs not) | Permissive — fallback record exists for both |
| IQBATTERY-5P-1P-NA-DOM | Serial number tier (3 ranges) | **Strict** — SN doesn't match any tier (not 54...) → FAIL |
| IQBATTERY-10C-1P-NA-DOM | Serial number range | Strict — both eligible/ineligible records exist; missing or unmatched SN → FAIL |
| IQ8HC-72-M-DOM-US | Multi-prefix SN range | Strict |
| IQ8MC-72-M-US | Multi-prefix SN range | Strict |
| IQ8PLUS-72-M-US | Multi-prefix SN range | Strict |

For strict resolution, missing or unmatched SNs result in `FAIL` because no fallback variant exists in the AVL. The customer must provide a valid SN matching one of the defined ranges.

### 9.7 Q.MI module-inverter pairing (special case)

The `Q.MI.349B-G1` inverter has two AVL records:
- `Q.MI.349B-G1` — used with all AC modules EXCEPT Q.TRON BLK M-G2+/AC
- `Q.MI.349B-G1 (for Q.TRON BLK M-G2+/AC)` — used ONLY with Q.TRON BLK M-G2+/AC modules

Customers always submit the bare SKU (`Q.MI.349B-G1`). The API auto-swaps to the Q.TRON variant if the module's Trimmed Name field in PVAVL is `Q.TRON BLK M-G2+/AC`. A `NOTE` is added to issues explaining the swap.

If a customer submits the variant SKU directly with a non-matching module, the API FAILs.

### 9.8 Unirac SolarMount stainless mid-clamp inheritance

Unirac SolarMount stainless steel mid-clamps are intentionally DCA-eligible without having their own DCA percentage. They inherit the End Clamp's DCA% when paired correctly.

**Detection** (a stainless SM mid-clamp):
- MSAVL Maker = "Unirac"
- MSAVL System Family contains "SolarMount"
- MSAVL Racking Product Name ends with "SS"
- Is on DCA AVL = True

**Inheritance rule**:
- If the BOM's End Clamp is DCA-eligible (on DCA AVL with a valid DCA%) → the stainless mid-clamp inherits the End Clamp's DCA%
- If the End Clamp is not DCA-eligible (missing from DCA AVL or has no DCA%) → the stainless mid-clamp contributes 0

A `NOTE` is added to the response issues explaining the inheritance:

> NOTE: Stainless Unirac SolarMount mid-clamp '<sku>' inherits DCA% 11.1% from paired End Clamp

---

## 10. Error Handling and HTTP Status Codes

### 10.1 Status codes

| Status | Meaning |
|---|---|
| 200 | Request was processed (regardless of valid=true/false). Check the response body. |
| 401 | Missing or invalid `X-API-Key` header. |
| 422 | Schema/shape error: malformed JSON, missing required field, wrong type. |
| 500 | Unhandled server error. Should not normally occur — report to SQT team. |

### 10.2 Distinguishing error types

The API distinguishes between request-shape errors (HTTP 422) and validation errors (HTTP 200 + `valid: false`):

- **HTTP 422**: the request couldn't be parsed against the schema. Example: `installation-date` missing, `bom` not an object, `quantity` is a string instead of an integer.
- **HTTP 200 + `valid: false`**: the request was parsed, but business validation failed. Example: SKU not in AVL, multi-inverter detected, missing required racking bucket.

Frontend logic should:
1. Check HTTP status. If 422, surface a generic "request format error" and log details.
2. If 200, parse the body. If `valid: false`, surface the issues array. If `valid: true`, surface the pass/fail flags and totals.

### 10.3 Common 422 causes

- `installation-date` missing or in an unparseable format (use `"YYYY-MM-DD"` or `"YYYY-MM-DDTHH:MM:SS"`)
- `bom.pv` not an array
- `bom.inverter` not an array
- `quantity` provided as a non-integer
- Top-level fields with wrong names (`installationDate` instead of `installation-date`, `BOM` instead of `bom`)

### 10.4 Common preflight FAILs (200 + valid:false)

- Missing required equipment buckets (Module, Inverter, Rail, Mid Clamp, End Clamp)
- Multiple distinct Module SKUs
- Multiple distinct inverter SKUs (manual review required)
- Battery present without `quantity` on PV item
- Both per-item and pooled identifiers specified for the same category

---

## 11. Limitations and Known Issues

### 11.1 Multi-inverter installations

Installations with two different inverter SKUs (mixed-capacity systems, e.g., 11.4kW primary + 3.8kW additional) are not currently supported automatically. The API responds with `FAIL: Multiple inverter SKUs require manual review`. These installs need human review until an averaging strategy is finalized.

### 11.2 Cold starts on Render

The API runs on Render. Free tier has cold starts (~30 seconds on first request after idle). The current Starter tier ($7/mo) does not have cold starts. If you experience timeouts on first request, contact the SQT team.

### 11.3 Airtable rate limits

The API fetches data from Airtable per request. High-volume request bursts may hit Airtable rate limits, causing slower responses. There is no caching layer currently.

### 11.4 Response time

Typical response time: 2-5 seconds (Airtable round-trips dominate). Larger BOMs with more racking SKUs are slower. There is currently no async/streaming option.

### 11.5 Test coverage and edge cases

Approximately 50 business cases are tested against the API on a regular cadence. Edge cases not yet covered:
- Mixed-vendor racking with cross-listing exceptions (Unirac + S-5! pairing)
- Three-inverter installations
- Custom carrier configurations not in MSAVL

If you encounter a case the API doesn't handle correctly, share the request payload with the SQT team. We maintain an Excel-driven test suite and add new cases as they're identified.

---

## Appendix A: Quick Reference Card

### Required request fields
- `installation-date` (string)
- `bom.pv` (≥1 item, single SKU)
- `bom.inverter` (≥1 item, single SKU)
- `other equipment.Rail`, `Mid Clamp`, `End Clamp`
- One-of: `Roof Flashing/Mount/Clamp` OR `L-foot / Standoff / Tilt-leg`

### Conditionally required
- `quantity` on PV BomItems when batteries are in the BOM

### Critical response fields
- `valid` — true if processable
- `pass_dca_pv`, `pass_dca_ess` — threshold pass/fail
- `pass_feoc_pv`, `pass_feoc_ess` — FEOC threshold pass/fail
- `unified_total_dca` — 2024 only, the IRS unified result
- `issues` — list of FAIL/WARNING/NOTE messages

### Issue prefixes
- `FAIL:` — request rejected
- `WARNING:` — non-fatal, math continues
- `NOTE:` — informational

### Contact

For questions, bug reports, or new test cases, contact the SQT team.
