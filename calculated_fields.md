# CBRE Dashboard — Tableau Calculated Fields Reference

All calculated fields used in the CBRE Market Intelligence Dashboard.
Use these directly in Tableau → Analysis → Create Calculated Field.

---

## 1. Demand Supply Gap (Thousands sq ft)

**Field Name:** `Demand Supply Gap (000 sq ft)`

```
[Demand Supply Gap (MSF)] * 1000
```

**Why:** Raw data is in MSF decimals (e.g., 0.2 = 200,000 sq ft).
Multiplying by 1000 makes KPI cards readable in thousands.

**Cyber City correction:** Value should display as **–200** (negative = oversupply)

---

## 2. Waterfall Chart Size Field

**Field Name:** `WF_Size`

```
-[Vacancy Compression]
```

**Why:** Tableau's Gantt Bar waterfall requires a negative size to show
downward bars. Vacancy compression is expressed as a positive rate;
negating it creates the correct visual direction.

**Usage:** Set as Size on Gantt Bar mark type.

---

## 3. Bullet Chart Benchmark

**Field Name:** `Max_Benchmark`

```
100
```

**Why:** Constant reference line for the bullet chart.
Represents the maximum benchmark leasing target (index = 100).

**Usage:** Add as a Reference Line on the Leasing axis.

---

## 4. Vacancy Rate Label (Formatted)

**Field Name:** `Vacancy Rate Label`

```
STR(ROUND([Vacancy Rate (%)] * 100, 1)) + "%"
```

**Usage:** Use on labels for dual-axis line chart.

---

## 5. Leasing Performance vs Benchmark (%)

**Field Name:** `Leasing vs Benchmark (%)`

```
([Total Leased Area] / [Max_Benchmark]) * 100
```

**Usage:** Used in bullet chart bar encoding.

---

## Notes

- All fields above are **worksheet-level** calculated fields
- Create them before building charts to avoid missing field errors
- Quarter field must be formatted as **discrete string** for heatmap row/column headers
- Corridor field is a **dimension** (string), not a measure

---

*Reference file for CBRE Tableau Dashboard — Rachit Bhatt*
