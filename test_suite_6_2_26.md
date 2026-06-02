# Solar Compatibility API — Test Suite

Verified passing cases as of 2026-06-02T17:04:32. Each case shows the JSON request body and the verified response. Use these as reference payloads for integration.

**Base URL:** `https://solar-compatibility-api.onrender.com/`

**Total passing cases:** 80

---

## excel_case_01_2024

_DCA + Non DCA_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE5700H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "242-02073-USA"
    ],
    "Mid Clamp": [
      "242-02071-USA"
    ],
    "Accessories": [
      "232-01106",
      "242-02168"
    ],
    "MLPE Mount": [
      "242-10034-USA"
    ],
    "Rail": [
      "232-10095-USA"
    ],
    "Splice": [
      "242-01213-USA"
    ],
    "Roof Flashing/Mount/Clamp": [
      "242-02729"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.306,
  "ess_side_total_dca": 0.481,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.4135,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE5700H-USMNBE78",
      "skus": null,
      "dca_pct": 0.176,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "232-10095-USA",
        "242-02071-USA",
        "242-02073-USA",
        "242-01213-USA",
        "242-02729",
        "242-10034-USA",
        "232-01106",
        "242-02168"
      ],
      "dca_pct": 0.086,
      "feoc_pct": null,
      "notes": [
        "Rail (232-10095-USA): 8.60%",
        "Mid Clamp (242-02071-USA): 11.10%",
        "End Clamp (242-02073-USA): 11.10%",
        "Splice (242-01213-USA): 11.10%",
        "Roof Flashing/Mount/Clamp (242-02729): 0.00%",
        "MLPE Mount (242-10034-USA): 0.00%",
        "Accessories (232-01106): no DCA %",
        "Accessories (242-02168): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "UBAT-10K1PS0B-03"
      ],
      "dca_pct": 0.481,
      "feoc_pct": null,
      "notes": [
        "BatteryA (UBAT-10K1PS0B-03): qty=1, capacity=9.7 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (41.4%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_01_2026

_DCA + Non DCA_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE5700H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "242-02073-USA"
    ],
    "MLPE Mount": [
      "242-10034-USA"
    ],
    "Mid Clamp": [
      "242-02071-USA"
    ],
    "Accessories": [
      "232-01106"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "242-02168"
    ],
    "Rail": [
      "232-10095-USA"
    ],
    "Splice": [
      "242-01213-USA"
    ],
    "Roof Flashing/Mount/Clamp": [
      "242-02729"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": false,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": 0.461,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": true,
  "pv_side_total_feoc": 0.679,
  "ess_side_total_feoc": 0.731,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE5700H-USMNBE78",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "232-10095-USA",
        "242-02071-USA",
        "242-02073-USA",
        "242-01213-USA",
        "242-02729",
        "242-02168",
        "242-10034-USA",
        "232-01106"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (232-10095-USA): 15.00%",
        "Mid Clamp (242-02071-USA): 3.50%",
        "End Clamp (242-02073-USA): 3.50%",
        "Splice (242-01213-USA): 3.50%",
        "Roof Flashing/Mount/Clamp (242-02729): no DCA %",
        "L-foot / Standoff / Tilt-leg (242-02168): 0.00%",
        "MLPE Mount (242-10034-USA): 3.50%",
        "Accessories (232-01106): no DCA %"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "UBAT-10K1PS0B-03"
      ],
      "dca_pct": 0.461,
      "feoc_pct": 0.731,
      "notes": [
        "BatteryA (UBAT-10K1PS0B-03): qty=1, capacity=9.7 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: ESS-side DCA 46.1% below threshold 50%"
  ]
}
```

---

## excel_case_02_2026

_multi vendor no crosslisting_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.C1+/AC 425",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-SQ-03-A1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "004FLCT6IN"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: IronRidge cannot be anchor \u2014 missing from Crosslisting of: 004FLCT6IN (Unirac)",
    "FAIL: Unirac cannot be anchor \u2014 missing from Crosslisting of: XR-10-168M-US (IronRidge), XR-MID-01-B1-US (IronRidge), UFO-END-01-B1-US (IronRidge), XR10-BOSS-01-M1-US (IronRidge), BHW-SQ-03-A1 (IronRidge), XR-LUG-04-A1 (IronRidge), BHW-MI-01-A1-US (IronRidge), XR-10-CAP01-B1 (IronRidge)"
  ]
}
```

---

## excel_case_03_2026

_unirac mid + end clamp (x) (missing equipment)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.C1+/AC 425",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "302021C-US"
    ],
    "Rail": [
      "315185M-US"
    ],
    "Splice": [
      "303019D-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "SHBUTYLD2-US"
    ],
    "MLPE Mount": [
      "MLPEMNT-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Missing required product type: Mid Clamp"
  ]
}
```

---

## excel_case_04a_2024

_unirac mid + unirac end clamp (o) (DCA eligible)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.C1+/AC 425",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "302021C-US"
    ],
    "Mid Clamp": [
      "302028D-US"
    ],
    "Rail": [
      "315185M-US"
    ],
    "Splice": [
      "303019D-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "SHBUTYLD2-US"
    ],
    "MLPE Mount": [
      "MLPEMNT-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.642,
  "ess_side_total_dca": 0.481,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.5314,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2.C1+/AC 425",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "Q.MI.349B-G1",
      "skus": null,
      "dca_pct": 0.34,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "302028D-US",
        "302028D-US",
        "302021C-US",
        "303019D-US",
        "SHBUTYLD2-US",
        "MLPEMNT-US"
      ],
      "dca_pct": 0.111,
      "feoc_pct": null,
      "notes": [
        "Mid Clamp (302028D-US): 11.10%",
        "Mid Clamp (302028D-US): 11.10%",
        "End Clamp (302021C-US): 11.10%",
        "Splice (303019D-US): 11.10%",
        "Roof Flashing/Mount/Clamp (SHBUTYLD2-US): 11.10%",
        "MLPE Mount (MLPEMNT-US): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "1707000-21-y"
      ],
      "dca_pct": 0.481,
      "feoc_pct": null,
      "notes": [
        "BatteryA (1707000-21-y): qty=1, capacity=13.5 kWh"
      ]
    }
  ],
  "issues": [
    "NOTE: Stainless Unirac SolarMount mid-clamp '302028D-US' inherits DCA% 11.1% from paired End Clamp",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (53.1%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_04a_2026

_unirac mid + unirac end clamp (o) (DCA eligible)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.C1+/AC 425",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "302021C-US"
    ],
    "Mid Clamp": [
      "302028D-US"
    ],
    "Rail": [
      "315185M-US"
    ],
    "Splice": [
      "303019D-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "SHBUTYLD2-US"
    ],
    "MLPE Mount": [
      "MLPEMNT-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": 0.595,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": true,
  "pv_side_total_feoc": 0.636,
  "ess_side_total_feoc": 0.677,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2.C1+/AC 425",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "Q.MI.349B-G1",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.205,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "302028D-US",
        "302028D-US",
        "302021C-US",
        "303019D-US",
        "SHBUTYLD2-US",
        "MLPEMNT-US"
      ],
      "dca_pct": 0.035,
      "feoc_pct": null,
      "notes": [
        "Mid Clamp (302028D-US): 3.50%",
        "Mid Clamp (302028D-US): 3.50%",
        "End Clamp (302021C-US): 3.50%",
        "Splice (303019D-US): 3.50%",
        "Roof Flashing/Mount/Clamp (SHBUTYLD2-US): 0.00%",
        "MLPE Mount (MLPEMNT-US): 3.50%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "1707000-21-y"
      ],
      "dca_pct": 0.595,
      "feoc_pct": 0.677,
      "notes": [
        "BatteryA (1707000-21-y): qty=1, capacity=13.5 kWh"
      ]
    }
  ],
  "issues": [
    "NOTE: Stainless Unirac SolarMount mid-clamp '302028D-US' inherits DCA% 3.5% from paired End Clamp"
  ]
}
```

---

## excel_case_04b_2024

_unirac mid + unirac end clamp (o) (DCA ineligible)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.C1+/AC 425",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "302021C"
    ],
    "Mid Clamp": [
      "302028D-US"
    ],
    "Rail": [
      "315185M-US"
    ],
    "Splice": [
      "303019D-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "SHBUTYLD2-US"
    ],
    "MLPE Mount": [
      "MLPEMNT-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.47,
  "ess_side_total_dca": 0.481,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.4776,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2.C1+/AC 425",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "Q.MI.349B-G1",
      "skus": null,
      "dca_pct": 0.34,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "315185M-US",
        "302028D-US",
        "302021C",
        "303019D-US",
        "SHBUTYLD2-US",
        "MLPEMNT-US"
      ],
      "dca_pct": 0.086,
      "feoc_pct": null,
      "notes": [
        "Rail (315185M-US): 8.60%",
        "Mid Clamp (302028D-US): 0.00%",
        "End Clamp (302021C): 0.00%",
        "Splice (303019D-US): 11.10%",
        "Roof Flashing/Mount/Clamp (SHBUTYLD2-US): 11.10%",
        "MLPE Mount (MLPEMNT-US): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "1707000-21-y"
      ],
      "dca_pct": 0.481,
      "feoc_pct": null,
      "notes": [
        "BatteryA (1707000-21-y): qty=1, capacity=13.5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (47.8%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_04b_2026

_unirac mid + unirac end clamp (o) (DCA ineligible)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.C1+/AC 425",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "302021C"
    ],
    "Mid Clamp": [
      "302028D-US"
    ],
    "Rail": [
      "315185M-US"
    ],
    "Splice": [
      "303019D-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "SHBUTYLD2-US"
    ],
    "MLPE Mount": [
      "MLPEMNT-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.468,
  "ess_side_total_dca": 0.595,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": true,
  "pv_side_total_feoc": 0.636,
  "ess_side_total_feoc": 0.677,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2.C1+/AC 425",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "Q.MI.349B-G1",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.205,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "315185M-US",
        "302028D-US",
        "302021C",
        "303019D-US",
        "SHBUTYLD2-US",
        "MLPEMNT-US"
      ],
      "dca_pct": 0.15,
      "feoc_pct": null,
      "notes": [
        "Rail (315185M-US): 15.00%",
        "Mid Clamp (302028D-US): 0.00%",
        "End Clamp (302021C): 0.00%",
        "Splice (303019D-US): 3.50%",
        "Roof Flashing/Mount/Clamp (SHBUTYLD2-US): 0.00%",
        "MLPE Mount (MLPEMNT-US): 3.50%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "1707000-21-y"
      ],
      "dca_pct": 0.595,
      "feoc_pct": 0.677,
      "notes": [
        "BatteryA (1707000-21-y): qty=1, capacity=13.5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "WARNING: PV-side DCA 46.8% below threshold 50%"
  ]
}
```

---

## excel_case_05_2024

_other stainless steel (mlpe attachment) used with fastener_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": []
      }
    ]
  },
  "other equipment": {
    "Rail": [
      "2012012"
    ],
    "End Clamp": [
      "2099039"
    ],
    "MLPE Mount": [
      "4011012"
    ],
    "Mid Clamp": [
      "2099022"
    ],
    "Accessories": [
      "3016017",
      "4011014"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "3016017"
    ],
    "Splice": [
      "2012013"
    ],
    "Roof Flashing/Mount/Clamp": [
      "2012026",
      "3011011"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.063,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.063,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "String",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.063,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "1707000-21-y",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "2012012",
        "2099022",
        "2099039",
        "2012013",
        "2012026",
        "3011011",
        "3016017",
        "4011012",
        "3016017",
        "4011014"
      ],
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": [
        "Rail (2012012): 0.00%",
        "Mid Clamp (2099022): 0.00%",
        "End Clamp (2099039): 0.00%",
        "Splice (2012013): 0.00%",
        "Roof Flashing/Mount/Clamp (2012026): 0.00%",
        "Roof Flashing/Mount/Clamp (3011011): 0.00%",
        "L-foot / Standoff / Tilt-leg (3016017): 0.00%",
        "MLPE Mount (4011012): no DCA %",
        "Accessories (3016017): 0.00%",
        "Accessories (4011014): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: Rails contribute 0 to DCA \u2014 not all rails are DCA eligible",
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (6.3%) compared to threshold (40%)",
    "WARNING: Combined DCA 6.3% below 2024 unified threshold 40%"
  ]
}
```

---

## excel_case_05_2026

_other stainless steel (mlpe attachment) used with fastener_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": []
      }
    ]
  },
  "other equipment": {
    "Rail": [
      "2012012"
    ],
    "End Clamp": [
      "2099039"
    ],
    "MLPE Mount": [
      "4011012"
    ],
    "Mid Clamp": [
      "2099022"
    ],
    "Accessories": [
      "3016017",
      "4011014"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "3016017"
    ],
    "Splice": [
      "2012013"
    ],
    "Roof Flashing/Mount/Clamp": [
      "2012026",
      "3011011"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.088,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": 0.574,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "String",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.088,
      "feoc_pct": 0.535,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "1707000-21-y",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": 0.039,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "2012012",
        "2099022",
        "2099039",
        "2012013",
        "2012026",
        "3011011",
        "3016017",
        "4011012",
        "3016017",
        "4011014"
      ],
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": [
        "Rail (2012012): 0.00%",
        "Mid Clamp (2099022): 0.00%",
        "End Clamp (2099039): 0.00%",
        "Splice (2012013): 0.00%",
        "Roof Flashing/Mount/Clamp (2012026): no DCA %",
        "Roof Flashing/Mount/Clamp (3011011): 0.00%",
        "L-foot / Standoff / Tilt-leg (3016017): 0.00%",
        "MLPE Mount (4011012): 0.00%",
        "Accessories (3016017): 0.00%",
        "Accessories (4011014): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: Rails contribute 0 to DCA \u2014 not all rails are DCA eligible",
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "WARNING: PV-side DCA 8.8% below threshold 50%"
  ]
}
```

---

## excel_case_06_2026

_sku not on avl / unknown sku_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420 fake",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE5700H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "Rail": [
      "2012012"
    ],
    "End Clamp": [
      "2099039"
    ],
    "MLPE Mount": [
      "4011012"
    ],
    "Mid Clamp": [
      "2099022"
    ],
    "Accessories": [
      "3016017"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "3016017"
    ],
    "Splice": [
      "2012013"
    ],
    "Roof Flashing/Mount/Clamp": [
      "2012026",
      "3011011",
      "4011014"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Roof Flashing/Mount/Clamp SKU '4011014' is not valid for this product type. Expected: fld9pUexOat7v3mKI in ['Other-Flashing', 'Other-Mount', 'Other-Rail Clamp', 'Other-Tile Mount']. Found: fld9pUexOat7v3mKI='Other-Accessory'",
    "FAIL: Module SKU 'Q.PEAK DUO BLK ML-G10.C+ 420 fake' not found in PVAVL"
  ]
}
```

---

## excel_case_07_2024

_S-5! + Ironridge_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE5700H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.306,
  "ess_side_total_dca": 0.481,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.4135,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE5700H-USMNBE78",
      "skus": null,
      "dca_pct": 0.176,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.086,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 8.60%",
        "Mid Clamp (XR-MID-01-B1-US): 11.10%",
        "End Clamp (UFO-END-01-B1-US): 11.10%",
        "Splice (XR10-BOSS-01-M1-US): 11.10%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): 0.00%",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): 0.00%",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 0.00%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "UBAT-10K1PS0B-03"
      ],
      "dca_pct": 0.481,
      "feoc_pct": null,
      "notes": [
        "BatteryA (UBAT-10K1PS0B-03): qty=1, capacity=9.7 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (41.4%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_07_2026

_S-5! + Ironridge_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE5700H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": false,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": 0.461,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": true,
  "pv_side_total_feoc": 0.679,
  "ess_side_total_feoc": 0.731,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE5700H-USMNBE78",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "UBAT-10K1PS0B-03"
      ],
      "dca_pct": 0.461,
      "feoc_pct": 0.731,
      "notes": [
        "BatteryA (UBAT-10K1PS0B-03): qty=1, capacity=9.7 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: ESS-side DCA 46.1% below threshold 50%"
  ]
}
```

---

## excel_case_08_2026

_DCA module + non DCA module_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "DCA.17 Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      },
      {
        "sku": "Q.PEAK DUO BLK ML-G10+",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (3800W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1",
      "XR-LUG-04-A1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-SQ-03-A1",
      "LFT-03-M1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Multiple Module SKUs not allowed (DCA.17 Q.PEAK DUO BLK ML-G10+ 415, Q.PEAK DUO BLK ML-G10+)",
    "FAIL: Missing required product type: Roof Flashing/Mount/Clamp"
  ]
}
```

---

## excel_case_09_2026

_sku not on avl / unknown sku_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.E1+/AC 440",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "MLPE Mount": [
      "PSR-MLP-US"
    ],
    "Mid Clamp": [
      "PSR-MCZ-US"
    ],
    "Accessories": [
      "PSR-CAP",
      "PSR-CBG",
      "PSR-WMC"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "PF-DRW85",
      "PSR-LUG"
    ],
    "Rail": [
      "PSR-M84-US"
    ],
    "Splice": [
      "PSR-SPLS-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "PIF2-BDT"
    ],
    "End Clamp": [
      "PSR-HEC"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Module SKU 'Q.TRON BLK M-G2.E1+/AC 440' not found in PVAVL"
  ]
}
```

---

## excel_case_10_2026

_No 5P SN / lower % of inverter for ACM (G2+/AC)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2+/AC 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "MLPE Mount": [
      "PSR-MLP-US"
    ],
    "Mid Clamp": [
      "PSR-MCZ-US"
    ],
    "End Clamp": [
      "PSR-HEC"
    ],
    "Accessories": [
      "PSR-CAP",
      "PSR-CBG",
      "PSR-WMC"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "PF-DRW85",
      "PSR-LUG"
    ],
    "Rail": [
      "PSR-M84"
    ],
    "Splice": [
      "PSR-SPLS-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "PIF2-BDT"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546) requires Serial Numbers for validation."
  ]
}
```

---

## excel_case_11_2024

_inverter + inverter (different wattage)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (11400W)",
        "serial_numbers": []
      },
      {
        "sku": "USE11400H-USSKBEZ8 (3800W)",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "PSR-MCZ-US"
    ],
    "MLPE Mount": [
      "PSR-MLP-US"
    ],
    "Mid Clamp": [
      "PSR-MCZ-US"
    ],
    "Accessories": [
      "PSR-CAP",
      "PSR-CBG",
      "PSR-LUG",
      "PSR-WMC"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "PF-DRW85"
    ],
    "Rail": [
      "PSR-M84-US"
    ],
    "Splice": [
      "PSR-SPLS-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "PIF2-BDT"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Multiple inverter SKUs require manual review"
  ]
}
```

---

## excel_case_11_2026

_inverter + inverter (different wattage)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (11400W)",
        "serial_numbers": []
      },
      {
        "sku": "USE11400H-USSKBEZ8 (3800W)",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "MLPE Mount": [
      "PSR-MLP-US"
    ],
    "Mid Clamp": [
      "PSR-MCZ-US"
    ],
    "End Clamp": [
      "PSR-MCZ-US"
    ],
    "Accessories": [
      "PSR-CAP",
      "PSR-CBG",
      "PSR-WMC"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "PF-DRW85",
      "PSR-LUG"
    ],
    "Rail": [
      "PSR-M84-US"
    ],
    "Splice": [
      "PSR-SPLS-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "PIF2-BDT"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Multiple inverter SKUs require manual review"
  ]
}
```

---

## excel_case_12_2024

_non DCA inverter_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.VOLT H7.6SX",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "PSR-MCZ-US"
    ],
    "MLPE Mount": [
      "PSR-MLP-US"
    ],
    "Mid Clamp": [
      "PSR-MCZ-US"
    ],
    "Accessories": [
      "PSR-CAP",
      "PSR-CBG",
      "PSR-LUG",
      "PSR-WMC"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "PF-DRW85"
    ],
    "Rail": [
      "PSR-M84-US"
    ],
    "Splice": [
      "PSR-SPLS-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "PIF2-BDT"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.186,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.186,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "String",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.063,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "Q.VOLT H7.6SX",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "PSR-M84-US",
        "PSR-MCZ-US",
        "PSR-MCZ-US",
        "PSR-SPLS-US",
        "PIF2-BDT",
        "PF-DRW85",
        "PSR-MLP-US",
        "PSR-CAP",
        "PSR-CBG",
        "PSR-LUG",
        "PSR-WMC"
      ],
      "dca_pct": 0.123,
      "feoc_pct": null,
      "notes": [
        "Rail (PSR-M84-US): 12.30%",
        "Mid Clamp (PSR-MCZ-US): 16.00%",
        "End Clamp (PSR-MCZ-US): 16.00%",
        "Splice (PSR-SPLS-US): 16.00%",
        "Roof Flashing/Mount/Clamp (PIF2-BDT): 0.00%",
        "L-foot / Standoff / Tilt-leg (PF-DRW85): 0.00%",
        "MLPE Mount (PSR-MLP-US): 0.00%",
        "Accessories (PSR-CAP): 0.00%",
        "Accessories (PSR-CBG): 0.00%",
        "Accessories (PSR-LUG): 0.00%",
        "Accessories (PSR-WMC): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (18.6%) compared to threshold (40%)",
    "WARNING: Combined DCA 18.6% below 2024 unified threshold 40%"
  ]
}
```

---

## excel_case_12_2026

_non DCA inverter_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.VOLT H7.6SX",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "4000145-US"
    ],
    "MLPE Mount": [
      "4000629-H-US"
    ],
    "Mid Clamp": [
      "4000145-US"
    ],
    "Accessories": [
      "4000176",
      "4000312"
    ],
    "Rail": [
      "4000819-US"
    ],
    "Splice": [
      "4000051-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "4000282"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.333,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": 0.535,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "String",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.088,
      "feoc_pct": 0.535,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "Q.VOLT H7.6SX",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "4000819-US",
        "4000145-US",
        "4000145-US",
        "4000051-US",
        "4000282",
        "4000629-H-US",
        "4000176",
        "4000312"
      ],
      "dca_pct": 0.245,
      "feoc_pct": null,
      "notes": [
        "Rail (4000819-US): 18.70%",
        "Mid Clamp (4000145-US): 4.40%",
        "End Clamp (4000145-US): 4.40%",
        "Splice (4000051-US): 4.40%",
        "Roof Flashing/Mount/Clamp (4000282): no DCA %",
        "MLPE Mount (4000629-H-US): 4.40%",
        "Accessories (4000176): 0.00%",
        "Accessories (4000312): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: PV-side DCA 33.3% below threshold 50%"
  ]
}
```

---

## excel_case_13_2024

_solaredge inverter + Tesla battery_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (10000W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "4000145-US"
    ],
    "MLPE Mount": [
      "4000629-H-US"
    ],
    "Mid Clamp": [
      "4000145-US"
    ],
    "Accessories": [
      "4000176",
      "4000312"
    ],
    "Rail": [
      "4000819-US"
    ],
    "Splice": [
      "4000051-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "4000282"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.486,
  "ess_side_total_dca": 0.481,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.4826,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE11400H-USSKBEZ8 (10000W)",
      "skus": null,
      "dca_pct": 0.356,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "4000819-US",
        "4000145-US",
        "4000145-US",
        "4000051-US",
        "4000282",
        "4000629-H-US",
        "4000176",
        "4000312"
      ],
      "dca_pct": 0.086,
      "feoc_pct": null,
      "notes": [
        "Rail (4000819-US): 8.60%",
        "Mid Clamp (4000145-US): 11.10%",
        "End Clamp (4000145-US): 11.10%",
        "Splice (4000051-US): 11.10%",
        "Roof Flashing/Mount/Clamp (4000282): 0.00%",
        "MLPE Mount (4000629-H-US): 0.00%",
        "Accessories (4000176): 0.00%",
        "Accessories (4000312): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "1707000-21-y"
      ],
      "dca_pct": 0.481,
      "feoc_pct": null,
      "notes": [
        "BatteryA (1707000-21-y): qty=1, capacity=13.5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (48.3%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_13_2026

_solaredge inverter + Tesla battery_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (10000W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "4000145-US"
    ],
    "MLPE Mount": [
      "4000629-H-US"
    ],
    "Mid Clamp": [
      "4000145-US"
    ],
    "Accessories": [
      "4000176",
      "4000312"
    ],
    "Rail": [
      "4000819-US"
    ],
    "Splice": [
      "4000051-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "4000282"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": 0.595,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": true,
  "pv_side_total_feoc": 0.679,
  "ess_side_total_feoc": 0.677,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE11400H-USSKBEZ8 (10000W)",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "4000819-US",
        "4000145-US",
        "4000145-US",
        "4000051-US",
        "4000282",
        "4000629-H-US",
        "4000176",
        "4000312"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (4000819-US): 15.00%",
        "Mid Clamp (4000145-US): 3.50%",
        "End Clamp (4000145-US): 3.50%",
        "Splice (4000051-US): 3.50%",
        "Roof Flashing/Mount/Clamp (4000282): no DCA %",
        "MLPE Mount (4000629-H-US): 3.50%",
        "Accessories (4000176): 0.00%",
        "Accessories (4000312): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "1707000-21-y"
      ],
      "dca_pct": 0.595,
      "feoc_pct": 0.677,
      "notes": [
        "BatteryA (1707000-21-y): qty=1, capacity=13.5 kWh"
      ]
    }
  ],
  "issues": []
}
```

---

## excel_case_14_2024

_enphase inverter + Tesla battery_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "5325476767"
        ]
      }
    ],
    "battery": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "Rail": [
      "XR-10-168B"
    ],
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "UFO-CL-01-B1"
    ],
    "Accessories": [
      "QM-JBX-RL02-B1",
      "XR-100-CAP01-B1",
      "XR-WC-01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-B1",
      "XR-LUG-04-A1"
    ],
    "Splice": [
      "XR100-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-F3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.384,
  "ess_side_total_dca": 0.481,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.4509,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
      "skus": null,
      "dca_pct": 0.34,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168B",
        "UFO-CL-01-B1",
        "UFO-END-01-B1-US",
        "XR100-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-F3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-B1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "QM-JBX-RL02-B1",
        "XR-100-CAP01-B1",
        "XR-WC-01-B1"
      ],
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168B): 0.00%",
        "Mid Clamp (UFO-CL-01-B1): 0.00%",
        "End Clamp (UFO-END-01-B1-US): 11.10%",
        "Splice (XR100-BOSS-01-M1-US): 11.10%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): 0.00%",
        "Roof Flashing/Mount/Clamp (QMTR-F3.25-A-12): 0.00%",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-B1): 0.00%",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 0.00%",
        "Accessories (QM-JBX-RL02-B1): 0.00%",
        "Accessories (XR-100-CAP01-B1): 0.00%",
        "Accessories (XR-WC-01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "1707000-21-y"
      ],
      "dca_pct": 0.481,
      "feoc_pct": null,
      "notes": [
        "BatteryA (1707000-21-y): qty=1, capacity=13.5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Rails contribute 0 to DCA \u2014 not all rails are DCA eligible",
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (45.1%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_14_2026

_enphase inverter + Tesla battery_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "5325476767"
        ]
      }
    ],
    "battery": [
      {
        "sku": "1707000-21-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "Rail": [
      "XR-10-168B"
    ],
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "UFO-CL-01-B1"
    ],
    "Accessories": [
      "QM-JBX-RL02-B1",
      "XR-100-CAP01-B1",
      "XR-WC-01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-B1",
      "XR-LUG-04-A1"
    ],
    "Splice": [
      "XR100-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-F3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.318,
  "ess_side_total_dca": 0.595,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": true,
  "pv_side_total_feoc": 0.679,
  "ess_side_total_feoc": 0.677,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168B",
        "UFO-CL-01-B1",
        "UFO-END-01-B1-US",
        "XR100-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-F3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-B1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "QM-JBX-RL02-B1",
        "XR-100-CAP01-B1",
        "XR-WC-01-B1"
      ],
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168B): 0.00%",
        "Mid Clamp (UFO-CL-01-B1): 0.00%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR100-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-F3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-B1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 0.00%",
        "Accessories (QM-JBX-RL02-B1): 0.00%",
        "Accessories (XR-100-CAP01-B1): 0.00%",
        "Accessories (XR-WC-01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "1707000-21-y"
      ],
      "dca_pct": 0.595,
      "feoc_pct": 0.677,
      "notes": [
        "BatteryA (1707000-21-y): qty=1, capacity=13.5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Rails contribute 0 to DCA \u2014 not all rails are DCA eligible",
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "WARNING: PV-side DCA 31.8% below threshold 50%"
  ]
}
```

---

## excel_case_15_2026

_missing optimizer_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (10000W)",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "ATH-01-M1"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: MLPE/Optimizer is required for SolarEdge MLPE inverters"
  ]
}
```

---

## excel_case_16_2026

_missing equipment_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [],
    "battery": []
  },
  "other equipment": {}
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Inverter SKU is required",
    "FAIL: Missing required product type: Rail",
    "FAIL: Missing required product type: Mid Clamp",
    "FAIL: Missing required product type: End Clamp",
    "FAIL: Missing required product type: Roof Flashing/Mount/Clamp"
  ]
}
```

---

## excel_case_17_2026

_sku not on avl / unknown sku (optimizer)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "SE7600H-USMNFBL75",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "242-02073-USA"
    ],
    "MLPE Mount": [
      "242-10034-USA"
    ],
    "Mid Clamp": [
      "242-02071-USA"
    ],
    "Accessories": [
      "232-01106",
      "242-02150"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "242-02168"
    ],
    "Rail": [
      "232-10095-USA"
    ],
    "Splice": [
      "242-01213-USA"
    ],
    "Roof Flashing/Mount/Clamp": [
      "242-02729"
    ],
    "MLPE/Optimizer": "fake_U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Inverter SKU 'SE7600H-USMNFBL75' not found in IAVL",
    "FAIL: MLPE/Optimizer SKU 'fake_U650-1GM4MRMU' not found in MLPEAVL"
  ]
}
```

---

## excel_case_18_2024

_DCA + Non DCA_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (10000W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      },
      {
        "sku": "BAT-10K1PS0B-02",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "Rail": [
      "084RLM1-US",
      "084RLM1"
    ],
    "End Clamp": [
      "CCLAMPM1"
    ],
    "MLPE Mount": [
      "MLPEMNT-US"
    ],
    "Mid Clamp": [
      "CCLAMPM1"
    ],
    "Accessories": [
      "ENDCAPD1",
      "WRMCLPD1"
    ],
    "Splice": [
      "RLSPLCM2"
    ],
    "Roof Flashing/Mount/Clamp": [
      "XTRABUTL-SH-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": false,
  "pv_side_total_dca": 0.356,
  "ess_side_total_dca": 0.2405,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.2678,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10+ 415",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE11400H-USSKBEZ8 (10000W)",
      "skus": null,
      "dca_pct": 0.356,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "084RLM1",
        "084RLM1-US",
        "CCLAMPM1",
        "CCLAMPM1",
        "RLSPLCM2",
        "XTRABUTL-SH-US",
        "MLPEMNT-US",
        "ENDCAPD1",
        "WRMCLPD1"
      ],
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": [
        "Rail (084RLM1): 0.00%",
        "Rail (084RLM1-US): 8.60%",
        "Mid Clamp (CCLAMPM1): 0.00%",
        "End Clamp (CCLAMPM1): 0.00%",
        "Splice (RLSPLCM2): 0.00%",
        "Roof Flashing/Mount/Clamp (XTRABUTL-SH-US): 11.10%",
        "MLPE Mount (MLPEMNT-US): 0.00%",
        "Accessories (ENDCAPD1): 0.00%",
        "Accessories (WRMCLPD1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "UBAT-10K1PS0B-03",
        "BAT-10K1PS0B-02"
      ],
      "dca_pct": 0.2405,
      "feoc_pct": null,
      "notes": [
        "BatteryA (UBAT-10K1PS0B-03): qty=1, capacity=9.7 kWh",
        "BatteryB (BAT-10K1PS0B-02): qty=1, capacity=9.7 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Rails contribute 0 to DCA \u2014 not all rails are DCA eligible",
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (26.8%) compared to threshold (40%)",
    "WARNING: Combined DCA 26.8% below 2024 unified threshold 40%"
  ]
}
```

---

## excel_case_18_2026

_DCA + Non DCA_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (10000W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      },
      {
        "sku": "BAT-10K1PS0B-02",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "Rail": [
      "084RLM1-US",
      "084RLM1"
    ],
    "End Clamp": [
      "CCLAMPM1"
    ],
    "MLPE Mount": [
      "008114M"
    ],
    "Mid Clamp": [
      "CCLAMPM1"
    ],
    "Accessories": [
      "ENDCAPD1",
      "WRMCLPD1"
    ],
    "Splice": [
      "RLSPLCM2"
    ],
    "Roof Flashing/Mount/Clamp": [
      "SHCLMPM2"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": false,
  "pv_side_total_dca": 0.248,
  "ess_side_total_dca": 0.2305,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": false,
  "pv_side_total_feoc": 0.617,
  "ess_side_total_feoc": 0.3655,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10+ 415",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": 0.369,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE11400H-USSKBEZ8 (10000W)",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "084RLM1",
        "084RLM1-US",
        "CCLAMPM1",
        "CCLAMPM1",
        "RLSPLCM2",
        "SHCLMPM2",
        "008114M",
        "ENDCAPD1",
        "WRMCLPD1"
      ],
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": [
        "Rail (084RLM1): 0.00%",
        "Rail (084RLM1-US): 15.00%",
        "Mid Clamp (CCLAMPM1): 0.00%",
        "End Clamp (CCLAMPM1): 0.00%",
        "Splice (RLSPLCM2): 0.00%",
        "Roof Flashing/Mount/Clamp (SHCLMPM2): no DCA %",
        "MLPE Mount (008114M): 0.00%",
        "Accessories (ENDCAPD1): 0.00%",
        "Accessories (WRMCLPD1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "UBAT-10K1PS0B-03",
        "BAT-10K1PS0B-02"
      ],
      "dca_pct": 0.2305,
      "feoc_pct": 0.3655,
      "notes": [
        "BatteryA (UBAT-10K1PS0B-03): qty=1, capacity=9.7 kWh",
        "BatteryB (BAT-10K1PS0B-02): qty=1, capacity=9.7 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Rails contribute 0 to DCA \u2014 not all rails are DCA eligible",
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "WARNING: PV-side DCA 24.8% below threshold 50%",
    "WARNING: ESS-side DCA 23.1% below threshold 50%",
    "WARNING: ESS-side FEOC 36.5% below threshold 55%"
  ]
}
```

---

## excel_case_19_2024

_non DCA + DCA expansion (pw3)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "1707000-11-y",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "1707000-11-y",
        "serial_numbers": [],
        "quantity": 1
      },
      {
        "sku": "1807000-20-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": false,
  "pv_side_total_dca": 0.123,
  "ess_side_total_dca": 0.3305,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.3026,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "String",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10+ 415",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "1707000-11-y",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.123,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 12.30%",
        "Mid Clamp (XR-MID-01-B1-US): 16.00%",
        "End Clamp (UFO-END-01-B1-US): 16.00%",
        "Splice (XR10-BOSS-01-M1-US): 16.00%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): 0.00%",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): 0.00%",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): 0.00%",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 0.00%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "1707000-11-y",
        "1807000-20-y"
      ],
      "dca_pct": 0.3305,
      "feoc_pct": null,
      "notes": [
        "BatteryA (1707000-11-y): qty=1, capacity=13.5 kWh",
        "BatteryExpansion (1807000-20-y): qty=1, capacity=13.5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (30.3%) compared to threshold (40%)",
    "WARNING: Combined DCA 30.3% below 2024 unified threshold 40%"
  ]
}
```

---

## excel_case_19_2026

_non DCA + DCA expansion (pw3)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "1707000-11-y",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "1707000-11-y",
        "serial_numbers": [],
        "quantity": 1
      },
      {
        "sku": "1807000-20-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.245,
  "ess_side_total_dca": 0.528,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": false,
  "pv_side_total_feoc": 0.457,
  "ess_side_total_feoc": 0.3385,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "String",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10+ 415",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": 0.457,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "1707000-11-y",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": 0.0,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.245,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 18.70%",
        "Mid Clamp (XR-MID-01-B1-US): 4.40%",
        "End Clamp (UFO-END-01-B1-US): 4.40%",
        "Splice (XR10-BOSS-01-M1-US): 4.40%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 4.40%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "1707000-11-y",
        "1807000-20-y"
      ],
      "dca_pct": 0.528,
      "feoc_pct": 0.3385,
      "notes": [
        "BatteryA (1707000-11-y): qty=1, capacity=13.5 kWh",
        "BatteryExpansion (1807000-20-y): qty=1, capacity=13.5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: PV-side DCA 24.5% below threshold 50%",
    "WARNING: ESS-side FEOC 33.9% below threshold 55%"
  ]
}
```

---

## excel_case_20_2026

_sku not on avl / unknown sku_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (11400W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UNX-BLCK-5K-A-01",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "302021D-US"
    ],
    "Mid Clamp": [
      "302027D-US"
    ],
    "Accessories": [
      "003251W"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "003251W"
    ],
    "Rail": [
      "315168M-US"
    ],
    "Splice": [
      "303019M-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "004BUTYLM-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Battery_0 SKU 'UNX-BLCK-5K-A-01' not found in BAVL"
  ]
}
```

---

## excel_case_21a_2024

_SN check for DCA eligibility (eligible)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+/TS 410 (with DCA eligible SN)",
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE10000H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "battery": [],
    "pv_serial_numbers": [
      "67672535",
      "6768253789"
    ]
  },
  "other equipment": {
    "Rail": [
      "084RLM1-US"
    ],
    "End Clamp": [
      "CCLAMPD1-US"
    ],
    "MLPE Mount": [
      "MLPEMNT-US"
    ],
    "Mid Clamp": [
      "CCLAMPD1-US"
    ],
    "Accessories": [
      "ENDCAPD1",
      "WRMCLPD1"
    ],
    "Splice": [
      "RLSPLCM2-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "XTRABUTL-SH-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.444,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.444,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10+/TS 410 (with DCA eligible SN)",
      "skus": null,
      "dca_pct": 0.01,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE10000H-USMNBE78",
      "skus": null,
      "dca_pct": 0.176,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "084RLM1-US",
        "CCLAMPD1-US",
        "CCLAMPD1-US",
        "RLSPLCM2-US",
        "XTRABUTL-SH-US",
        "MLPEMNT-US",
        "ENDCAPD1",
        "WRMCLPD1"
      ],
      "dca_pct": 0.258,
      "feoc_pct": null,
      "notes": [
        "Rail (084RLM1-US): 8.60%",
        "Mid Clamp (CCLAMPD1-US): 11.10%",
        "End Clamp (CCLAMPD1-US): 11.10%",
        "Splice (RLSPLCM2-US): 11.10%",
        "Roof Flashing/Mount/Clamp (XTRABUTL-SH-US): 11.10%",
        "MLPE Mount (MLPEMNT-US): 0.00%",
        "Accessories (ENDCAPD1): 0.00%",
        "Accessories (WRMCLPD1): 0.00%"
      ]
    }
  ],
  "issues": [
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (44.4%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_21b_2024

_SN check for DCA eligibility (Base variant)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+/TS 410",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE10000H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "Rail": [
      "084RLM1-US"
    ],
    "End Clamp": [
      "CCLAMPD1-US"
    ],
    "MLPE Mount": [
      "MLPEMNT-US"
    ],
    "Mid Clamp": [
      "CCLAMPD1-US"
    ],
    "Accessories": [
      "ENDCAPD1",
      "WRMCLPD1"
    ],
    "Splice": [
      "RLSPLCM2-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "XTRABUTL-SH-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.434,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.434,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10+/TS 410",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE10000H-USMNBE78",
      "skus": null,
      "dca_pct": 0.176,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "084RLM1-US",
        "CCLAMPD1-US",
        "CCLAMPD1-US",
        "RLSPLCM2-US",
        "XTRABUTL-SH-US",
        "MLPEMNT-US",
        "ENDCAPD1",
        "WRMCLPD1"
      ],
      "dca_pct": 0.258,
      "feoc_pct": null,
      "notes": [
        "Rail (084RLM1-US): 8.60%",
        "Mid Clamp (CCLAMPD1-US): 11.10%",
        "End Clamp (CCLAMPD1-US): 11.10%",
        "Splice (RLSPLCM2-US): 11.10%",
        "Roof Flashing/Mount/Clamp (XTRABUTL-SH-US): 11.10%",
        "MLPE Mount (MLPEMNT-US): 0.00%",
        "Accessories (ENDCAPD1): 0.00%",
        "Accessories (WRMCLPD1): 0.00%"
      ]
    }
  ],
  "issues": [
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (43.4%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_21c_2024

_SN check for DCA eligibility (ineligible SN)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+/TS 410 (with DCA eligible SN)",
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE10000H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "battery": [],
    "pv_serial_numbers": [
      "67672535",
      "6768253789",
      "6768243789"
    ]
  },
  "other equipment": {
    "Rail": [
      "084RLM1-US"
    ],
    "End Clamp": [
      "CCLAMPD1-US"
    ],
    "MLPE Mount": [
      "MLPEMNT-US"
    ],
    "Mid Clamp": [
      "CCLAMPD1-US"
    ],
    "Accessories": [
      "ENDCAPD1",
      "WRMCLPD1"
    ],
    "Splice": [
      "RLSPLCM2-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "XTRABUTL-SH-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: The following serial numbers did not fit the rule: ['6768243789']"
  ]
}
```

---

## excel_case_21a_2026

_SN check for DCA eligibility_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+/TS 410 (with DCA eligible SN)",
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE10000H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "pv_serial_numbers": [
      "67672535",
      "6768253789"
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.452,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": 0.617,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10+/TS 410 (with DCA eligible SN)",
      "skus": null,
      "dca_pct": 0.008,
      "feoc_pct": 0.369,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE10000H-USMNBE78",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: PV-side DCA 45.2% below threshold 50%"
  ]
}
```

---

## excel_case_21b_2026

_SN check for DCA eligibility (no SN)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+/TS 410",
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE10000H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "pv_serial_numbers": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.444,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": 0.617,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10+/TS 410",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": 0.369,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE10000H-USMNBE78",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: PV-side DCA 44.4% below threshold 50%"
  ]
}
```

---

## excel_case_22_2024

_DCA eligiblity determined by material code_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "DCA.17 Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [
          "3535017"
        ],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (3800W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1",
      "XR-LUG-04-A1"
    ],
    "Roof Flashing/Mount/Clamp": [
      "FLSH-01-B1-US"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.637,
  "ess_side_total_dca": 0.481,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.5407,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "DCA.17 Q.PEAK DUO BLK ML-G10+ 415",
      "skus": null,
      "dca_pct": 0.023,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE11400H-USSKBEZ8 (3800W)",
      "skus": null,
      "dca_pct": 0.356,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "FLSH-01-B1-US",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1",
        "XR-LUG-04-A1"
      ],
      "dca_pct": 0.258,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 8.60%",
        "Mid Clamp (XR-MID-01-B1-US): 11.10%",
        "End Clamp (UFO-END-01-B1-US): 11.10%",
        "Splice (XR10-BOSS-01-M1-US): 11.10%",
        "Roof Flashing/Mount/Clamp (FLSH-01-B1-US): 11.10%",
        "MLPE Mount (BHW-MI-01-A1-US): 0.00%",
        "Accessories (XR-10-CAP01-B1): 0.00%",
        "Accessories (XR-LUG-04-A1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "UBAT-10K1PS0B-03"
      ],
      "dca_pct": 0.481,
      "feoc_pct": null,
      "notes": [
        "BatteryA (UBAT-10K1PS0B-03): qty=1, capacity=9.7 kWh"
      ]
    }
  ],
  "issues": [
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (54.1%) compared to threshold (40%)"
  ]
}
```

---

## Q.PEAK_fails_MC_validation

_DCA eligiblity determined by material code fail_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "DCA.17 Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [
          "3535018"
        ],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (3800W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1",
      "XR-LUG-04-A1"
    ],
    "Roof Flashing/Mount/Clamp": [
      "FLSH-01-B1-US"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: The following material codes did not fit the rule: ['3535018']"
  ]
}
```

---

## excel_case_22_2026

_DCA eligiblity determined by material code_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "DCA.17 Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [
          "3535017"
        ],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (3800W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "FLSH-01-B1-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": false,
  "pv_side_total_dca": 0.483,
  "ess_side_total_dca": 0.461,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": true,
  "pv_side_total_feoc": 0.617,
  "ess_side_total_feoc": 0.731,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "DCA.17 Q.PEAK DUO BLK ML-G10+ 415",
      "skus": null,
      "dca_pct": 0.039,
      "feoc_pct": 0.369,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE11400H-USSKBEZ8 (3800W)",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "FLSH-01-B1-US",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1",
        "XR-LUG-04-A1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (FLSH-01-B1-US): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%",
        "Accessories (XR-LUG-04-A1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "UBAT-10K1PS0B-03"
      ],
      "dca_pct": 0.461,
      "feoc_pct": 0.731,
      "notes": [
        "BatteryA (UBAT-10K1PS0B-03): qty=1, capacity=9.7 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: PV-side DCA 48.3% below threshold 50%",
    "WARNING: ESS-side DCA 46.1% below threshold 50%"
  ]
}
```

---

## excel_case_23_2024

_G2+/AC + MI : check the %_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2+/AC 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1 (for Q.TRON BLK M-G2+/AC)",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.246,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.246,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2+/AC 420",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "Q.MI.349B-G1 (for Q.TRON BLK M-G2+/AC)",
      "skus": null,
      "dca_pct": 0.16,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.086,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 8.60%",
        "Mid Clamp (XR-MID-01-B1-US): 11.10%",
        "End Clamp (UFO-END-01-B1-US): 11.10%",
        "Splice (XR10-BOSS-01-M1-US): 11.10%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): 0.00%",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): 0.00%",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): 0.00%",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 0.00%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (24.6%) compared to threshold (40%)",
    "WARNING: Combined DCA 24.6% below 2024 unified threshold 40%"
  ]
}
```

---

## excel_case_23_2026

_G2+/AC + MI : check the %_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2+/AC 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1 (for Q.TRON BLK M-G2+/AC)",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.392,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": 0.574,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2+/AC 420",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": 0.369,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "Q.MI.349B-G1 (for Q.TRON BLK M-G2+/AC)",
      "skus": null,
      "dca_pct": 0.196,
      "feoc_pct": 0.205,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: PV-side DCA 39.2% below threshold 50%"
  ]
}
```

---

## excel_case_24_2024

_Enphase SN - fail_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
        "serial_numbers": [
          "542515059404"
        ]
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.47,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.47,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
      "skus": null,
      "dca_pct": 0.34,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.086,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 8.60%",
        "Mid Clamp (XR-MID-01-B1-US): 11.10%",
        "End Clamp (UFO-END-01-B1-US): 11.10%",
        "Splice (XR10-BOSS-01-M1-US): 11.10%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): 0.00%",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): 0.00%",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): 0.00%",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 0.00%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (47.0%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_24_2026

_Enphase SN - fail_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
        "serial_numbers": [
          "542515059404"
        ]
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": 0.431,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.0,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    }
  ],
  "issues": []
}
```

---

## excel_case_25_2024

_Enphase SN - pass_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "532513040740"
        ]
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.47,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.47,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
      "skus": null,
      "dca_pct": 0.34,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.086,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 8.60%",
        "Mid Clamp (XR-MID-01-B1-US): 11.10%",
        "End Clamp (UFO-END-01-B1-US): 11.10%",
        "Splice (XR10-BOSS-01-M1-US): 11.10%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): 0.00%",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): 0.00%",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): 0.00%",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 0.00%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (47.0%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_25_2026

_Enphase SN - pass_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "532513040740"
        ]
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": 0.679,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    }
  ],
  "issues": []
}
```

---

## excel_case_26_2024

_Enphase SN - fail + Enphase battery pass_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
        "serial_numbers": [
          "542515059404"
        ]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "quantity": 1,
        "serial_numbers": [
          "542673100745"
        ]
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.47,
  "ess_side_total_dca": 0.546,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.5043,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
      "skus": null,
      "dca_pct": 0.34,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.086,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 8.60%",
        "Mid Clamp (XR-MID-01-B1-US): 11.10%",
        "End Clamp (UFO-END-01-B1-US): 11.10%",
        "Splice (XR10-BOSS-01-M1-US): 11.10%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): 0.00%",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): 0.00%",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): 0.00%",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 0.00%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)"
      ],
      "dca_pct": 0.546,
      "feoc_pct": null,
      "notes": [
        "BatteryA (IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)): qty=1, capacity=5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (50.4%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_26_2026

_Enphase SN - fail + Enphase battery pass_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
        "serial_numbers": [
          "542515059404"
        ]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "quantity": 1,
        "serial_numbers": [
          "542673100745"
        ]
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": 0.568,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": true,
  "pv_side_total_feoc": 0.431,
  "ess_side_total_feoc": 0.568,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.0,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)"
      ],
      "dca_pct": 0.568,
      "feoc_pct": 0.568,
      "notes": [
        "BatteryA (IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)): qty=1, capacity=5 kWh"
      ]
    }
  ],
  "issues": []
}
```

---

## excel_case_27_2024

_Enphase SN - pass + Enphase bettery fail (both pass in 2024)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "532513040740"
        ]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx < 2529)",
        "quantity": 1,
        "serial_numbers": [
          "542523100745"
        ]
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.47,
  "ess_side_total_dca": 0.456,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.4637,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
      "skus": null,
      "dca_pct": 0.34,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.086,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 8.60%",
        "Mid Clamp (XR-MID-01-B1-US): 11.10%",
        "End Clamp (UFO-END-01-B1-US): 11.10%",
        "Splice (XR10-BOSS-01-M1-US): 11.10%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): 0.00%",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): 0.00%",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): 0.00%",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 0.00%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx < 2529)"
      ],
      "dca_pct": 0.456,
      "feoc_pct": null,
      "notes": [
        "BatteryA (IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx < 2529)): qty=1, capacity=5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (46.4%) compared to threshold (40%)"
  ]
}
```

---

## excel_case_27_2026

_Enphase SN - pass + Enphase bettery fail_

**Request:**

```json
{
  "installation-date": "2026-06-15",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "532513040740"
        ]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx < 2529)",
        "quantity": 1,
        "serial_numbers": [
          "542523100745"
        ]
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": false,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": 0.436,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": false,
  "pv_side_total_feoc": 0.679,
  "ess_side_total_feoc": 0.0,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx < 2529)"
      ],
      "dca_pct": 0.436,
      "feoc_pct": 0.0,
      "notes": [
        "BatteryA (IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx < 2529)): qty=1, capacity=5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: ESS-side DCA 43.6% below threshold 50%",
    "WARNING: ESS-side FEOC 0.0% below threshold 55%"
  ]
}
```

---

## excel_case_28_2024

_Enphase non-DOM sku_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-US",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA (SN does not begin with 54)",
        "quantity": 1,
        "serial_numbers": [
          "522523100745"
        ]
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "4000145-US"
    ],
    "MLPE Mount": [
      "4000629-H-US"
    ],
    "Mid Clamp": [
      "4000145-US"
    ],
    "Accessories": [
      "4000176",
      "4000312"
    ],
    "Rail": [
      "4000819-US"
    ],
    "Splice": [
      "4000051-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "4000282"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": false,
  "pv_side_total_dca": 0.29,
  "ess_side_total_dca": 0.0,
  "dca_pv_threshold": 0.4,
  "dca_ess_threshold": 0.4,
  "unified_total_dca": 0.1592,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.044,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-US",
      "skus": null,
      "dca_pct": 0.16,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "4000819-US",
        "4000145-US",
        "4000145-US",
        "4000051-US",
        "4000282",
        "4000629-H-US",
        "4000176",
        "4000312"
      ],
      "dca_pct": 0.086,
      "feoc_pct": null,
      "notes": [
        "Rail (4000819-US): 8.60%",
        "Mid Clamp (4000145-US): 11.10%",
        "End Clamp (4000145-US): 11.10%",
        "Splice (4000051-US): 11.10%",
        "Roof Flashing/Mount/Clamp (4000282): 0.00%",
        "MLPE Mount (4000629-H-US): 0.00%",
        "Accessories (4000176): 0.00%",
        "Accessories (4000312): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "IQBATTERY-5P-1P-NA (SN does not begin with 54)"
      ],
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": [
        "BatteryA (IQBATTERY-5P-1P-NA (SN does not begin with 54)): qty=1, capacity=5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "NOTE: 2024 uses unified DCA check \u2014 combined PV+ESS sum (15.9%) compared to threshold (40%)",
    "WARNING: Combined DCA 15.9% below 2024 unified threshold 40%"
  ]
}
```

---

## excel_case_28_2026

_Enphase non-DOM sku_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-US",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA (SN begins with 54)",
        "quantity": 1,
        "serial_numbers": []
      }
    ],
    "battery_serial_numbers": [
      "542523100745"
    ]
  },
  "other equipment": {
    "End Clamp": [
      "4000145-US"
    ],
    "MLPE Mount": [
      "4000629-H-US"
    ],
    "Mid Clamp": [
      "4000145-US"
    ],
    "Accessories": [
      "4000176",
      "4000312"
    ],
    "Rail": [
      "4000819-US"
    ],
    "Splice": [
      "4000051-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "4000282"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": false,
  "pv_side_total_dca": 0.462,
  "ess_side_total_dca": 0.107,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": false,
  "pv_side_total_feoc": 0.431,
  "ess_side_total_feoc": 0.0,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "IQ8HC-72-M-US",
      "skus": null,
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "4000819-US",
        "4000145-US",
        "4000145-US",
        "4000051-US",
        "4000282",
        "4000629-H-US",
        "4000176",
        "4000312"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (4000819-US): 15.00%",
        "Mid Clamp (4000145-US): 3.50%",
        "End Clamp (4000145-US): 3.50%",
        "Splice (4000051-US): 3.50%",
        "Roof Flashing/Mount/Clamp (4000282): no DCA %",
        "MLPE Mount (4000629-H-US): 3.50%",
        "Accessories (4000176): 0.00%",
        "Accessories (4000312): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "IQBATTERY-5P-1P-NA (SN begins with 54)"
      ],
      "dca_pct": 0.107,
      "feoc_pct": 0.0,
      "notes": [
        "BatteryA (IQBATTERY-5P-1P-NA (SN begins with 54)): qty=1, capacity=5 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: PV-side DCA 46.2% below threshold 50%",
    "WARNING: ESS-side DCA 10.7% below threshold 50%",
    "WARNING: ESS-side FEOC 0.0% below threshold 55%"
  ]
}
```

---

## excel_case_29_2024

_inverter only (SEDG)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (11400W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: MLPE/Optimizer is required for SolarEdge MLPE inverters"
  ]
}
```

---

## excel_case_29_2026

_inverter only (SEDG)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (11400W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: MLPE/Optimizer is required for SolarEdge MLPE inverters"
  ]
}
```

---

## excel_case_30_2026

_optimizer only ( w/o inverter)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Inverter SKU is required"
  ]
}
```

---

## excel_case_31_2026

_Expansion unit only_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
        "serial_numbers": [
          "53215567"
        ]
      }
    ],
    "battery": [
      {
        "sku": "1807000-20-y",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Expansion battery requires a non-expansion base unit"
  ]
}
```

---

## excel_case_32_2024

_Enphase SN (no SN provided)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
        "serial_numbers": []
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546) requires Serial Numbers for validation"
  ]
}
```

---

## excel_case_33_2024

_Enphase SN (ineligible SN provided)_

**Request:**

```json
{
  "installation-date": "2024-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
        "serial_numbers": [
          "676767676767"
        ]
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: The following serial numbers did not fit the rule: ['676767676767']"
  ]
}
```

---

## blank_sku_pv_fails

_blank PV SKU_

**Request:**

```json
{
  "installation-date": "2026-06-15",
  "bom": {
    "pv": [
      {
        "sku": "",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US",
        "serial_numbers": [
          "532513040740"
        ]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM",
        "quantity": 1,
        "serial_numbers": [
          "542523100745"
        ]
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Module SKU is required"
  ]
}
```

---

## blank_sku_inv_fails

_Elank Inverter SKU should show that missing_

**Request:**

```json
{
  "installation-date": "2026-06-15",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "",
        "serial_numbers": [
          "532513040740"
        ]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "quantity": 1,
        "serial_numbers": [
          "542555100745"
        ]
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Inverter SKU is required"
  ]
}
```

---

## blank_sku_mlpemnt_fails

_Blank sku on Mlpe mount should show that as missing_

**Request:**

```json
{
  "installation-date": "2026-06-15",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx >= 2501 OR 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "532513040740"
        ]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "quantity": 1,
        "serial_numbers": [
          "542555100745"
        ]
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      ""
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: MLPE Mount is required for MLPE/microinverter systems"
  ]
}
```

---

## sedg_non_dca_optimizer

_inverter_dca_should_be_zero_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10+ 415",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE11400H-USSKBEZ8 (10000W)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "UBAT-10K1PS0B-03",
        "serial_numbers": [],
        "quantity": 1
      },
      {
        "sku": "BAT-10K1PS0B-02",
        "serial_numbers": [],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "Rail": [
      "084RLM1-US",
      "084RLM1"
    ],
    "End Clamp": [
      "CCLAMPM1"
    ],
    "MLPE Mount": [
      "MLPEMNT-US"
    ],
    "Mid Clamp": [
      "CCLAMPM1"
    ],
    "Accessories": [
      "ENDCAPD1",
      "WRMCLPD1"
    ],
    "Splice": [
      "RLSPLCM2"
    ],
    "Roof Flashing/Mount/Clamp": [
      "XTRABUTL-SH-US"
    ],
    "MLPE/Optimizer": "S440"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": false,
  "pv_side_total_dca": 0.0,
  "ess_side_total_dca": 0.2305,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": false,
  "pv_side_total_feoc": 0.617,
  "ess_side_total_feoc": 0.3655,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.PEAK DUO BLK ML-G10+ 415",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": 0.369,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE11400H-USSKBEZ8 (10000W)",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "084RLM1",
        "084RLM1-US",
        "CCLAMPM1",
        "CCLAMPM1",
        "RLSPLCM2",
        "XTRABUTL-SH-US",
        "MLPEMNT-US",
        "ENDCAPD1",
        "WRMCLPD1"
      ],
      "dca_pct": 0.0,
      "feoc_pct": null,
      "notes": [
        "Rail (084RLM1): 0.00%",
        "Rail (084RLM1-US): 15.00%",
        "Mid Clamp (CCLAMPM1): 0.00%",
        "End Clamp (CCLAMPM1): 0.00%",
        "Splice (RLSPLCM2): 0.00%",
        "Roof Flashing/Mount/Clamp (XTRABUTL-SH-US): 0.00%",
        "MLPE Mount (MLPEMNT-US): 3.50%",
        "Accessories (ENDCAPD1): 0.00%",
        "Accessories (WRMCLPD1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "UBAT-10K1PS0B-03",
        "BAT-10K1PS0B-02"
      ],
      "dca_pct": 0.2305,
      "feoc_pct": 0.3655,
      "notes": [
        "BatteryA (UBAT-10K1PS0B-03): qty=1, capacity=9.7 kWh",
        "BatteryB (BAT-10K1PS0B-02): qty=1, capacity=9.7 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: Rails contribute 0 to DCA \u2014 not all rails are DCA eligible",
    "WARNING: Fasteners contribute 0 to DCA \u2014 not all fasteners are DCA eligible",
    "WARNING: PV-side DCA 0.0% below threshold 50%",
    "WARNING: ESS-side DCA 23.1% below threshold 50%",
    "WARNING: ESS-side FEOC 36.5% below threshold 55%"
  ]
}
```

---

## enphase_inv_wrong_sn_for_variant

_Fails due to having incorrect serial numbers provided._

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8MC-72-M-US (SN begins with 53xxxx OR 54xxxx where xxxx < 2546)"
      }
    ],
    "battery": [],
    "inverter_serial_numbers": [
      "532513040740",
      "529191929"
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: The following serial numbers did not fit the rule: ['529191929']"
  ]
}
```

---

## enphase_inv_sn_not_provided

_Fails due to having no serial numbers provided._

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8MC-72-M-US (SN begins with 53xxxx OR 54xxxx where xxxx < 2546)"
      }
    ],
    "battery": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: IQ8MC-72-M-US (SN begins with 53xxxx OR 54xxxx where xxxx < 2546) requires Serial Numbers for validation"
  ]
}
```

---

## Q.MI_mismatch_1

_G2+/AC must be used with specific Q.MI variant_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2+/AC 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "542547994"
        ],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "MLPE Mount": [
      "PSR-MLP-US"
    ],
    "Mid Clamp": [
      "PSR-MCZ-US"
    ],
    "End Clamp": [
      "PSR-HEC"
    ],
    "Accessories": [
      "PSR-CAP",
      "PSR-CBG",
      "PSR-WMC"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "PF-DRW85",
      "PSR-LUG"
    ],
    "Rail": [
      "PSR-M84"
    ],
    "Splice": [
      "PSR-SPLS-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "PIF2-BDT"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Q.TRON BLK M-G2+/AC modules can only be used with SKU: Q.MI.349B-G1 (for Q.TRON BLK M-G2+/AC)."
  ]
}
```

---

## Q.MI_mismatch_2

_nonregular Q.MI used with regular AC module_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.C1+/AC 425",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1 (for Q.TRON BLK M-G2+/AC)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "542547994"
        ],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "MLPE Mount": [
      "PSR-MLP-US"
    ],
    "Mid Clamp": [
      "PSR-MCZ-US"
    ],
    "End Clamp": [
      "PSR-HEC"
    ],
    "Accessories": [
      "PSR-CAP",
      "PSR-CBG",
      "PSR-WMC"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "PF-DRW85",
      "PSR-LUG"
    ],
    "Rail": [
      "PSR-M84"
    ],
    "Splice": [
      "PSR-SPLS-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "PIF2-BDT"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: All other AC modules can only be used with SKU: Q.MI.349B-G1."
  ]
}
```

---

## Q.MI_mismatch_3

_Q.MI variant used with DC module_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1 (for Q.TRON BLK M-G2+/AC)",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "542547994"
        ],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "MLPE Mount": [
      "PSR-MLP-US"
    ],
    "Mid Clamp": [
      "PSR-MCZ-US"
    ],
    "End Clamp": [
      "PSR-HEC"
    ],
    "Accessories": [
      "PSR-CAP",
      "PSR-CBG",
      "PSR-WMC"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "PF-DRW85",
      "PSR-LUG"
    ],
    "Rail": [
      "PSR-M84"
    ],
    "Splice": [
      "PSR-SPLS-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "PIF2-BDT"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: DC modules are not compatible with Q.MI-series inverters."
  ]
}
```

---

## Q.MI_mismatch_4

_Q.MI regular used with DC module_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "542547994"
        ],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "MLPE Mount": [
      "PSR-MLP-US"
    ],
    "Mid Clamp": [
      "PSR-MCZ-US"
    ],
    "End Clamp": [
      "PSR-HEC"
    ],
    "Accessories": [
      "PSR-CAP",
      "PSR-CBG",
      "PSR-WMC"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "PF-DRW85",
      "PSR-LUG"
    ],
    "Rail": [
      "PSR-M84"
    ],
    "Splice": [
      "PSR-SPLS-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "PIF2-BDT"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: DC modules are not compatible with Q.MI-series inverters."
  ]
}
```

---

## battery_SEDG_mismatched_sn

_One SN does not match rule_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.VOLT H7.6SX",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "542547994",
          "542537342"
        ],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "MLPE Mount": [
      "PSR-MLP-US"
    ],
    "Mid Clamp": [
      "PSR-MCZ-US"
    ],
    "End Clamp": [
      "PSR-HEC"
    ],
    "Accessories": [
      "PSR-CAP",
      "PSR-CBG",
      "PSR-WMC"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "PF-DRW85",
      "PSR-LUG"
    ],
    "Rail": [
      "PSR-M84"
    ],
    "Splice": [
      "PSR-SPLS-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "PIF2-BDT"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: The following serial numbers did not fit the rule: ['542537342']"
  ]
}
```

---

## battery_pooling_model_mismatch

_One Serial Number should be missed by pooled batteries._

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
        "serial_numbers": [
          "542515059404"
        ]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "quantity": 1,
        "serial_numbers": [
          "542673100745"
        ]
      },
      {
        "sku": "IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "quantity": 1
      }
    ],
    "battery_serial_numbers": [
      "542673100745",
      "542673100747",
      "542777777"
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: BatteryB must be same model as BatteryA"
  ]
}
```

---

## battery_pooling_correct_fail

_One Serial Number should be missed by pooled batteries._

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
        "serial_numbers": [
          "542515059404"
        ]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "quantity": 1
      },
      {
        "sku": "IQBATTERY-5P-1P-NA (SN begins with 54)",
        "quantity": 1
      }
    ],
    "battery_serial_numbers": [
      "542673100745",
      "542673100747",
      "6767676767"
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Some pooled Serial numbers were not associated with one of the provided batteries. ['6767676767'] is a list of the unmatched Serial Numbers."
  ]
}
```

---

## battery_not_pooled_correct_fail

_Serial numbers not pooled so failure will be different._

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)",
        "serial_numbers": [
          "542515059404"
        ]
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "quantity": 1,
        "serial_numbers": [
          "542673100745",
          "542673100747"
        ]
      },
      {
        "sku": "IQBATTERY-5P-1P-NA (SN begins with 54)",
        "quantity": 1,
        "serial_numbers": [
          "542673100747",
          "6767676767"
        ]
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: The following serial numbers did not fit the rule: ['6767676767']"
  ]
}
```

---

## inverter_pooled_correct_fail

_Serial numbers pooled for inverter_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.PEAK DUO BLK ML-G10.C+ 420",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "IQ8HC-72-M-DOM-US (SN begins with 53xxxx where xxxx < 2501 OR 54xxxx where xxxx < 2546)"
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-5P-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "quantity": 1,
        "serial_numbers": [
          "542673100745",
          "542673100747"
        ]
      },
      {
        "sku": "IQBATTERY-5P-1P-NA (SN begins with 54)",
        "quantity": 1,
        "serial_numbers": [
          "542673100747"
        ]
      }
    ],
    "inverter_serial_numbers": [
      "53240567",
      "53251067"
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: The following serial numbers did not fit the rule: ['53251067']"
  ]
}
```

---

## SN_membership_list_2026_pass

_SN check for DCA eligibility within membership list (there)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2+ 430 (with DCA eligible SN)",
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE10000H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "pv_serial_numbers": [
      "205224472502701180",
      "204824452502704128",
      "205524497502700189"
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.452,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": 0.617,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2+ 430 (with DCA eligible SN)",
      "skus": null,
      "dca_pct": 0.008,
      "feoc_pct": 0.369,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE10000H-USMNBE78",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: PV-side DCA 45.2% below threshold 50%"
  ]
}
```

---

## SN_membership_list_base_2026_pass

_SN check for DCA eligibility within membership list (non DCA eligible variant)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2+ 430",
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE10000H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "pv_serial_numbers": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": null,
  "pv_side_total_dca": 0.444,
  "ess_side_total_dca": null,
  "dca_pv_threshold": 0.5,
  "dca_ess_threshold": 0.5,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": 0.617,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": 0.4,
  "feoc_ess_threshold": 0.55,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2+ 430",
      "skus": null,
      "dca_pct": 0.0,
      "feoc_pct": 0.369,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE10000H-USMNBE78",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "BHW-TB-03-A1",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (BHW-TB-03-A1): 0.00%",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    }
  ],
  "issues": [
    "WARNING: PV-side DCA 44.4% below threshold 50%"
  ]
}
```

---

## SN_membership_list_2026_fail

_SN check for DCA eligibility within membership list (not there)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2+ 430 (with DCA eligible SN)",
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE10000H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "pv_serial_numbers": [
      "6767676767",
      "205224472502701180",
      "204824452502704128",
      "205524497502700189"
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: The following serial numbers did not fit the rule: ['6767676767']"
  ]
}
```

---

## SN_membership_list_2026_fail_np

_SN check for DCA eligibility within membership list (not provided)_

**Request:**

```json
{
  "installation-date": "2026-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2+ 430 (with DCA eligible SN)",
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE10000H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "pv_serial_numbers": []
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "BHW-TB-03-A1",
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": false,
  "pass_dca_pv": null,
  "pass_dca_ess": null,
  "pv_side_total_dca": null,
  "ess_side_total_dca": null,
  "dca_pv_threshold": null,
  "dca_ess_threshold": null,
  "unified_total_dca": null,
  "pass_feoc_pv": null,
  "pass_feoc_ess": null,
  "pv_side_total_feoc": null,
  "ess_side_total_feoc": null,
  "feoc_pv_threshold": null,
  "feoc_ess_threshold": null,
  "system_type": null,
  "components": [],
  "issues": [
    "FAIL: Q.TRON BLK M-G2+ 430 (with DCA eligible SN) requires Serial Numbers for validation"
  ]
}
```

---

## 2027_pass_case

_S-5! + Ironridge_

**Request:**

```json
{
  "installation-date": "2027-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.D+ 430",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE5700H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "542674343"
        ],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.563,
  "ess_side_total_dca": 0.568,
  "dca_pv_threshold": 0.55,
  "dca_ess_threshold": 0.55,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": false,
  "pv_side_total_feoc": 0.679,
  "ess_side_total_feoc": 0.568,
  "feoc_pv_threshold": 0.45,
  "feoc_ess_threshold": 0.6,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2.D+ 430",
      "skus": null,
      "dca_pct": 0.119,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE5700H-USMNBE78",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)"
      ],
      "dca_pct": 0.568,
      "feoc_pct": 0.568,
      "notes": [
        "BatteryA (IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)): qty=1, capacity=10 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: ESS-side FEOC 56.8% below threshold 60%"
  ]
}
```

---

## 2027_pass_ESS_only_case

_S-5! + Ironridge_

**Request:**

```json
{
  "installation-date": "2027-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.C+ 435",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "USE5700H-USMNBE78",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "542674343"
        ],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ],
    "MLPE/Optimizer": "U650-1GM4MRMU"
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": false,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.514,
  "ess_side_total_dca": 0.568,
  "dca_pv_threshold": 0.55,
  "dca_ess_threshold": 0.55,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": false,
  "pv_side_total_feoc": 0.679,
  "ess_side_total_feoc": 0.568,
  "feoc_pv_threshold": 0.45,
  "feoc_ess_threshold": 0.6,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2.C+ 435",
      "skus": null,
      "dca_pct": 0.07,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "USE5700H-USMNBE78",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.248,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)"
      ],
      "dca_pct": 0.568,
      "feoc_pct": 0.568,
      "notes": [
        "BatteryA (IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)): qty=1, capacity=10 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: PV-side DCA 51.4% below threshold 55%",
    "WARNING: ESS-side FEOC 56.8% below threshold 60%"
  ]
}
```

---

## 2027_pass_case_AC

_S-5! + Ironridge_

**Request:**

```json
{
  "installation-date": "2027-06-15T00:00:00",
  "bom": {
    "pv": [
      {
        "sku": "Q.TRON BLK M-G2.D1+/AC 430",
        "serial_numbers": [],
        "material_codes": [],
        "quantity": 10
      }
    ],
    "inverter": [
      {
        "sku": "Q.MI.349B-G1",
        "serial_numbers": []
      }
    ],
    "battery": [
      {
        "sku": "IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)",
        "serial_numbers": [
          "542674343"
        ],
        "quantity": 1
      }
    ]
  },
  "other equipment": {
    "End Clamp": [
      "UFO-END-01-B1-US"
    ],
    "Mid Clamp": [
      "XR-MID-01-B1-US"
    ],
    "Accessories": [
      "XR-10-CAP01-B1"
    ],
    "L-foot / Standoff / Tilt-leg": [
      "LFT-03-M1",
      "XR-LUG-04-A1"
    ],
    "Rail": [
      "XR-10-168M-US"
    ],
    "Splice": [
      "XR10-BOSS-01-M1-US"
    ],
    "Roof Flashing/Mount/Clamp": [
      "QMTR-BM-A-12",
      "QMTR-S3.25-A-12"
    ],
    "MLPE Mount": [
      "BHW-MI-01-A1-US"
    ]
  }
}
```

**Response:**

```json
{
  "valid": true,
  "pass_dca_pv": true,
  "pass_dca_ess": true,
  "pv_side_total_dca": 0.563,
  "ess_side_total_dca": 0.568,
  "dca_pv_threshold": 0.55,
  "dca_ess_threshold": 0.55,
  "unified_total_dca": null,
  "pass_feoc_pv": true,
  "pass_feoc_ess": false,
  "pv_side_total_feoc": 0.636,
  "ess_side_total_feoc": 0.568,
  "feoc_pv_threshold": 0.45,
  "feoc_ess_threshold": 0.6,
  "system_type": "MLPE",
  "components": [
    {
      "key": "Module",
      "sku": "Q.TRON BLK M-G2.D1+/AC 430",
      "skus": null,
      "dca_pct": 0.119,
      "feoc_pct": 0.431,
      "notes": []
    },
    {
      "key": "Inverter",
      "sku": "Q.MI.349B-G1",
      "skus": null,
      "dca_pct": 0.248,
      "feoc_pct": 0.205,
      "notes": []
    },
    {
      "key": "Racking",
      "sku": null,
      "skus": [
        "XR-10-168M-US",
        "XR-MID-01-B1-US",
        "UFO-END-01-B1-US",
        "XR10-BOSS-01-M1-US",
        "QMTR-BM-A-12",
        "QMTR-S3.25-A-12",
        "LFT-03-M1",
        "XR-LUG-04-A1",
        "BHW-MI-01-A1-US",
        "XR-10-CAP01-B1"
      ],
      "dca_pct": 0.196,
      "feoc_pct": null,
      "notes": [
        "Rail (XR-10-168M-US): 15.00%",
        "Mid Clamp (XR-MID-01-B1-US): 3.50%",
        "End Clamp (UFO-END-01-B1-US): 3.50%",
        "Splice (XR10-BOSS-01-M1-US): 3.50%",
        "Roof Flashing/Mount/Clamp (QMTR-BM-A-12): no DCA %",
        "Roof Flashing/Mount/Clamp (QMTR-S3.25-A-12): no DCA %",
        "L-foot / Standoff / Tilt-leg (LFT-03-M1): no DCA %",
        "L-foot / Standoff / Tilt-leg (XR-LUG-04-A1): 0.00%",
        "MLPE Mount (BHW-MI-01-A1-US): 3.50%",
        "Accessories (XR-10-CAP01-B1): 0.00%"
      ]
    },
    {
      "key": "ESS",
      "sku": null,
      "skus": [
        "IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)"
      ],
      "dca_pct": 0.568,
      "feoc_pct": 0.568,
      "notes": [
        "BatteryA (IQBATTERY-10C-1P-NA-DOM (SN begins with 54xxxx where xxxx >= 2546)): qty=1, capacity=10 kWh"
      ]
    }
  ],
  "issues": [
    "WARNING: ESS-side FEOC 56.8% below threshold 60%"
  ]
}
```

---

