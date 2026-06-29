# CBRE Dashboard — Step-by-Step Tableau Build Guide

## Prerequisites
- Tableau Desktop 2022.1+
- File: `CBRE_Dashboard_v2.xlsx`
- Screen resolution: 1920×1080 recommended

---

## STEP 1: Connect Data

1. Open Tableau → Connect → Microsoft Excel
2. Select `CBRE_Dashboard_v2.xlsx`
3. Drag `Office_Leasing` to the canvas (primary table)

---

## STEP 2: Set Up Joins

### Join 1 — Office_Leasing + Vacancy_Rental
- Drag `Vacancy_Rental` next to `Office_Leasing`
- Join type: **Left Join**
- Join key: `Quarter = Quarter`
- ✅ Do NOT add Corridor to this join

### Join 2 — Office_Leasing + Early_Warning
- Drag `Early_Warning` to canvas
- Join type: **Left Join**
- Join key: `Corridor = Corridor`
- ✅ Do NOT add Quarter to this join

### Join 3 — Office_Leasing + Residential
- Drag `Residential` to canvas
- Join type: **Left Join**
- Join key: `Quarter = Quarter`

---

## STEP 3: Create Calculated Fields

Go to **Analysis → Create Calculated Field** for each:

```
Name: Demand Supply Gap (000 sq ft)
Formula: [Demand Supply Gap (MSF)] * 1000
```

```
Name: WF_Size
Formula: -[Vacancy Compression]
```

```
Name: Max_Benchmark
Formula: 100
```

---

## STEP 4: Build Sheet 1 — KPI Cards

1. Create 4 separate worksheets (one per KPI)
2. For each: drag measure to **Text** mark
3. Format: Font size 36, bold, color `#3D5059`
4. Remove all gridlines, borders
5. Add label below in smaller font (12pt, gray)

**KPIs:**
- Total Leasing Area (SUM of Total Leased Area)
- Avg Rental Value (AVG of Rental Value)
- Avg Vacancy Rate (AVG of Vacancy Rate)
- Demand Supply Gap — use `Demand Supply Gap (000 sq ft)` field

---

## STEP 5: Build Sheet 2 — Leasing by Corridor (Bar Chart)

1. Rows: `SUM(Total Leased Area)`
2. Columns: `Corridor` (discrete)
3. Sort: Descending by leased area
4. Mark type: Bar
5. Color: `#3D5059`
6. Add data labels on bars

---

## STEP 6: Build Sheet 3 — CH2 Scatter (Supply vs Demand)

> ⚠️ Use Office_Leasing fields ONLY for this chart

1. Columns: `Supply`
2. Rows: `Demand`
3. Detail: `Corridor`
4. Size: `Leasing Volume`
5. Color: `Corridor` (categorical)
6. Add reference line: X=Y (equal supply/demand line)

---

## STEP 7: Build Sheet 4 — Vacancy & Rental Trend (Dual-Axis)

1. Columns: `Quarter` (ordered)
2. Rows: `AVG(Vacancy Rate (%))` → drag `AVG(Rental Value)` to right axis
3. Right-click second axis → **Synchronize Axis** (uncheck if scales differ)
4. Mark types: Both Line
5. Color: Vacancy = `#3D5059`, Rental = `#E8A030` (amber accent)

---

## STEP 8: Build Sheet 5 — Early Warning Heatmap

1. Rows: `Corridor`
2. Columns: `Risk Signal Category`
3. Mark type: **Square**
4. Color: `Signal Intensity` (sequential palette, low=light, high=dark red)
5. **Cell sizing:** Press `Ctrl + Shift + B` to enter Text Cell mode, then resize

---

## STEP 9: Build Sheet 6 — Bullet Chart (Leasing vs Benchmark)

1. Columns: `SUM(Total Leased Area)`
2. Rows: `Corridor`
3. Mark type: Bar
4. Color: `#3D5059`
5. Add Reference Line:
   - Scope: Per Cell
   - Value: `Max_Benchmark` constant (100)
   - Line style: Solid, dark gray
   - Label: None

---

## STEP 10: Build Sheet 7 — Waterfall Chart (Vacancy Compression)

1. Columns: `Corridor`
2. Rows: `SUM(WF_Size)`
3. Mark type: **Gantt Bar**
4. Size: `WF_Size` field
5. Color: Conditional — negative = red (`#C0392B`), positive = teal (`#3D5059`)
6. Add zero reference line

---

## STEP 11: Assemble Dashboard

1. New Dashboard → Fixed size: **1200 × 900 px**
2. Layout:
   ```
   [ KPI Card 1 ] [ KPI Card 2 ] [ KPI Card 3 ] [ KPI Card 4 ]
   [ Bar Chart — Leasing by Corridor          ] [ Scatter CH2 ]
   [ Dual-Axis Trend                          ] [ Heatmap     ]
   [ Bullet Chart         ] [ Waterfall Chart              ]
   ```
3. Add CBRE logo placeholder (top-left) — color block `#3D5059`
4. Dashboard title: "CBRE Market Intelligence Dashboard"
   - Font: Arial 20pt Bold, color `#3D5059`
5. Background: White (`#FFFFFF`)
6. Add thin border `#E0E0E0` around each chart container

---

## STEP 12: Final Formatting Checklist

- [ ] All axis titles removed or simplified
- [ ] Gridlines removed from bar/scatter charts
- [ ] Tooltips customized with field names (no Sheet names)
- [ ] KPI cards have no borders
- [ ] Font consistent: Arial throughout
- [ ] Color: `#3D5059` as primary, no blue/green defaults
- [ ] Dashboard title visible and aligned
- [ ] Legend placed bottom-right, compact

---

*Build guide for CBRE Tableau Dashboard — Rachit Bhatt*
