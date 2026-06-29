# CBRE Dashboard — Data Schema & Join Logic

## File: CBRE_Dashboard_v2.xlsx

---

## Sheet Schemas

### 1. Office_Leasing
| Column | Type | Description |
|---|---|---|
| Quarter | String | Time period (e.g., Q1 2024) |
| Corridor | String | Geographic corridor (e.g., Cyber City, Golf Course Road) |
| Total Leased Area | Number | Total area leased in sq ft |
| Supply | Number | Available supply in sq ft |
| Demand | Number | Demand in sq ft |
| Demand Supply Gap (MSF) | Decimal | Gap in million sq ft (raw) |
| Leasing Volume | Number | Count of transactions |

---

### 2. Residential
| Column | Type | Description |
|---|---|---|
| Quarter | String | Time period |
| Segment | String | Housing type (Luxury, Mid, Affordable) |
| Units Sold | Number | Volume of units |
| Average Price (₹/sq ft) | Number | Avg price per sq ft |

---

### 3. Vacancy_Rental
| Column | Type | Description |
|---|---|---|
| Quarter | String | Time period |
| Vacancy Rate (%) | Decimal | Vacancy as % of total stock |
| Rental Value (₹/sq ft/month) | Number | Avg monthly rental |

> ⚠️ **No Corridor column.** Join to Office_Leasing on Quarter ONLY.

---

### 4. Early_Warning
| Column | Type | Description |
|---|---|---|
| Corridor | String | Geographic corridor |
| Risk Signal Category | String | Type of risk (Vacancy Spike, Demand Drop, etc.) |
| Signal Intensity | Number | 1–5 scale (1=low, 5=critical) |

> ⚠️ **No Quarter column.** Join to Office_Leasing on Corridor ONLY.

---

### 5. KPI_Cards
| Column | Type | Description |
|---|---|---|
| KPI Name | String | Metric label |
| Value | Number | Aggregated value |
| Unit | String | Display unit |
| Period | String | Reporting period |

---

### 6. LEGEND
| Column | Type | Description |
|---|---|---|
| Item | String | Reference item name |
| Value | Number | Constant or reference value |
| Notes | String | Context/notes |

**Key constants from LEGEND:**
- `Max_Benchmark` = 100

---

## Join Diagram

```
Office_Leasing ──── [Quarter] ──── Vacancy_Rental
       │
       └────────── [Corridor] ──── Early_Warning
       │
       └────────── [Quarter] ──── Residential
```

---

## Common Mistakes to Avoid

| Mistake | Impact | Fix |
|---|---|---|
| Join Vacancy_Rental on Corridor | No Corridor column → join fails or nulls | Use Quarter only |
| Join Early_Warning on Quarter | No Quarter column → row explosion | Use Corridor only |
| Use MSF values in KPI cards directly | Values like 0.2 show instead of 200 | Multiply by 1000 |
| Cyber City Gap shown as +200 | Incorrect — it's oversupply | Value should be –200 |

---

*Data documentation for CBRE Tableau Dashboard — Rachit Bhatt*
