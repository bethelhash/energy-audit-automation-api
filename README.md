# Energy Audit Automation API

**Commercial building energy screening with multi-city Building Performance Standards compliance.**  
NYC LL97 · Boston BERDO 2.0 · Denver Energize Denver · EPA ENERGY STAR benchmarks · Every penalty cited to statute.

[![RapidAPI](https://img.shields.io/badge/RapidAPI-Subscribe-0055DA?style=flat-square)](https://rapidapi.com/bethelnedi/api/energy-audit-automation-api)
[![Demo](https://img.shields.io/badge/Live_Tool-BuildingIQ-FFD21E?style=flat-square)](https://buildingiq-nu.vercel.app/)
[![Docs](https://img.shields.io/badge/API_Docs-Swagger-85EA2D?style=flat-square)](https://amfumu-energy-audit-api.hf.space/docs)

---

## The Compliance Problem

Building Performance Standards are now **enforceable law** in 40+ US cities. Non-compliant buildings pay annual penalties calculated on every tonne of CO₂e they emit over their limit. The 2030 limits are 40–60% stricter than today's.

| City | Law | Penalty Rate | Covers |
|------|-----|-------------|--------|
| New York City | Local Law 97 | $268/tCO₂e over limit | Buildings ≥ 25,000 sq ft |
| Boston | BERDO 2.0 | $234/tCO₂e + $1,000/day | Non-res ≥ 20,000 sq ft |
| Denver | Energize Denver | $0.30/kBtu over EUI target | Buildings ≥ 25,000 sq ft |

This API calculates your exposure under all three simultaneously — current period and 2030.

---

## Quick Start

```bash
# Quick screen from monthly bill (Free)
curl -X POST https://energy-audit-automation-api.p.rapidapi.com/audit/quick \
  -H "X-RapidAPI-Key: YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "property_type": "office",
    "sq_ft": 75000,
    "monthly_energy_cost_usd": 14000,
    "city": "nyc"
  }'

# Full audit with actual utility data (Pro)
curl -X POST https://energy-audit-automation-api.p.rapidapi.com/audit/full \
  -H "X-RapidAPI-Key: YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "property_type": "office",
    "sq_ft": 75000,
    "annual_kwh": 1250000,
    "annual_therms": 8500,
    "city": "all",
    "grid_region": "NYISO"
  }'
```

---

## What You Get Back

```json
{
  "eui": { "site_eui": 68.4, "source_eui": 142.1 },
  "benchmark": { "rating": "below_average", "pct_vs_median": "+22%" },
  "carbon": { "total_mtco2e": 412.7, "mtco2e_per_sqft": 0.00550 },
  "compliance": {
    "ll97": {
      "compliant_2024": false,
      "annual_penalty_2024_usd": 43218,
      "compliant_2030": false,
      "annual_penalty_2030_usd": 118650
    }
  },
  "upgrade_priorities": [
    {
      "name": "HVAC system upgrade",
      "typical_eui_savings_pct": 18,
      "simple_payback_yr": 4.2,
      "source": "ASHRAE 90.1-2019; DOE Better Buildings 2023"
    }
  ]
}
```

---

## Endpoints

| Method | Endpoint | Plan | Description |
|--------|----------|------|-------------|
| `POST` | `/audit/quick` | Free | EUI screen from monthly bill |
| `POST` | `/audit/full` | Pro | Full audit + multi-city BPS penalties + upgrade roadmap |
| `GET` | `/reference/property-types` | Free | 17 building types with EPA median EUI |
| `GET` | `/reference/cities` | Free | BPS cities, laws, and penalty structures |
| `GET` | `/reference/ll97-limits` | Free | NYC LL97 limits by building type, both periods |
| `GET` | `/reference/carbon-factors` | Free | EPA eGRID 2022 emission factors by grid region |

---

## Data Sources

| Data | Source |
|------|--------|
| EPA median EUI by building type | EPA ENERGY STAR Portfolio Manager Technical Reference (Aug 2024) |
| LL97 carbon coefficients | NYC Admin Code §28-320 / 1 RCNY §103-14 |
| BERDO limits and penalties | Boston Municipal Code §7-2.2 (amended 2023) |
| Energize Denver EUI targets | Denver Revised Municipal Code §§4-38 et seq. |
| Grid emission factors | EPA eGRID 2022 Table 2 |
| Natural gas emission factor | EPA 40 CFR Part 98 Table C-1 (53.06 kgCO₂/MMBtu) |
| Building energy consumption | DOE CBECS 2018 Table E1 |
| Upgrade savings benchmarks | ASHRAE 90.1-2019; DOE Better Buildings Initiative 2023 |

---

## Supported Property Types

`office` `retail` `hotel` `multifamily` `warehouse` `hospital` `school` `data_center` `manufacturing` `laboratory` `supermarket` `worship` `dormitory` `courthouse` `bank` `restaurant` `fitness`

---

## Plans

| Plan | Price | Calls |
|------|-------|-------|
| Free | $0/mo | 5/min |
| Pro | $99/mo | 1,000/hr |

[Subscribe on RapidAPI →](https://rapidapi.com/bethelnedi/api/energy-audit-automation-api)

---

## Topics

`energy-audit` `building-performance-standards` `ll97` `berdo` `energize-denver` `eui` `energy-use-intensity` `commercial-buildings` `carbon-emissions` `ashrae` `epa-energy-star` `building-compliance` `ghg-emissions` `nyc-ll97` `boston-berdo` `solar-offset` `fastapi` `python` `rapidapi`
