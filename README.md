# CBRE
🏢 CBRE Market Intelligence Dashboard — Tableau Project
Role: Data Analyst Candidate | Round: Interview Assignment (Round 2)  
Tool: Tableau Desktop | Data: CBRE_Dashboard_v2.xlsx (6 sheets)  
Brand Color: `#3D5059` | Dashboard Theme: CBRE Corporate
---
📌 Project Overview
This Tableau dashboard was built as part of the CBRE Round 2 interview assignment. The goal was to design a Market Intelligence Dashboard for CBRE's real estate portfolio using multi-sheet data joins, advanced chart types, and CBRE brand styling.
The dashboard covers:
Office Leasing performance across corridors
Residential market trends
Vacancy & Rental rate analysis
Early Warning Signals for market risk
KPI Summary Cards
---
📂 Data Source
File: `CBRE\_Dashboard\_v2.xlsx`
Sheet Name	Description
`Office\_Leasing`	Leasing volume, area, corridor-wise data
`Residential`	Residential transactions and pricing
`Vacancy\_Rental`	Vacancy rates and rental values by quarter
`Early\_Warning`	Corridor-level risk signals
`KPI\_Cards`	Aggregated KPI metrics
`LEGEND`	Reference values and benchmark constants
---
🔗 Data Relationships & Join Logic
Join	Key Field	Notes
`Office\_Leasing` ↔ `Vacancy\_Rental`	`Quarter`	No Corridor column in Vacancy_Rental
`Office\_Leasing` ↔ `Early\_Warning`	`Corridor`	No Quarter column in Early_Warning
`Office\_Leasing` ↔ `Residential`	`Quarter`	Residential trends aligned to leasing periods
> ⚠️ \*\*Critical:\*\* Use Quarter-only join for Vacancy\_Rental; use Corridor-only join for Early\_Warning. Cross-joins on wrong fields will cause data inflation.
---
📊 Dashboard Views & Chart Types
1. KPI Cards (Top Row)
Total Leasing Area (sq ft)
Average Rental Value
Average Vacancy Rate
Demand Supply Gap (thousands sq ft)
> 💡 Demand Supply Gap raw values are in MSF decimals — multiply by 1000 to display in thousands sq ft.  
> Cyber City corrected value: \*\*–200 thousand sq ft\*\*
---
2. Office Leasing by Corridor — Bar Chart
X-axis: Corridor
Y-axis: Total Leased Area
Color: CBRE brand `#3D5059`
---
3. CH2 Scatter Plot — Supply vs Demand
Uses Office_Leasing fields only
X: Supply (sq ft)
Y: Demand (sq ft)
Size: Leasing Volume
Color by Corridor
---
4. Vacancy & Rental Trend — Dual-Axis Line Chart
X: Quarter
Y1: Vacancy Rate (%)
Y2: Rental Value (₹/sq ft)
Synchronized axes
---
5. Early Warning Heatmap
Rows: Corridor
Columns: Risk Signal Category
Color: Intensity scale (low → high risk)
Cell sizing: Text Cell option (`Ctrl + Shift + B`)
---
6. Bullet Chart — Leasing vs Benchmark
Bar: Actual Leasing
Reference Line: `Max\_Benchmark = 100` (constant)
Color: CBRE `#3D5059`
---
7. Waterfall Chart — Vacancy Compression
Calculated Field: `WF\_Size = -\[Vacancy Compression]`
Shows corridor-wise compression in vacancy
Gantt Bar mark type
---
🧮 Key Calculated Fields
```tableau
// Demand Supply Gap (in thousands sq ft)
\[Demand Supply Gap (000 sq ft)] = \[Demand Supply Gap (MSF)] \* 1000

// Waterfall size
\[WF\_Size] = -\[Vacancy Compression]

// Bullet chart reference
\[Max\_Benchmark] = 100
```
---
🎨 Design & Branding
Element	Value
Primary Color	`#3D5059` (CBRE Corporate)
Font	Tableau default / Arial
Background	White
Border/Lines	Light gray `#E0E0E0`
Dashboard Size	Fixed — 1200 × 900 px
> ❌ Do \*\*not\*\* use `#003087` — that is JLL's brand color, not CBRE's.
---
💡 Build Notes & Lessons Learned
Multi-sheet joins in Tableau require careful key selection — wrong join fields cause row multiplication
Heatmap cell sizing — use Text Cell (Ctrl+Shift+B) not manual sizing
Waterfall charts in Tableau use Gantt Bar mark with a negative size field
Bullet charts need a constant reference line, not a dynamic measure
KPI Cards — use BANs (Big A** Numbers) with custom formatting for executive-level readability
Vacancy_Rental sheet has no Corridor column — joining on Quarter only is intentional
Early_Warning sheet has no Quarter column — joining on Corridor only is intentional
---
🏗️ Project Context
This dashboard was self-initiated and presented in CBRE Round 1 as a Gurugram NCR Market Intelligence concept. Round 2 required building it fully in Tableau with the provided dataset.
Industry: Commercial Real Estate (CRE)
Company: CBRE Group, Inc.
Domain: Market Intelligence, Portfolio Analytics
---
👤 Author
Rachit Bhatt  
MBA — Finance & Business Analytics | Delhi Technological University (2025)  
Data Analyst | rachitbhatt.lovable.app  
GitHub: github.com/rachitbhatt16  
LinkedIn: linkedin.com/in/rachitbhatt0016
---
This project was built as part of a structured interview process. All data is provided by CBRE for assessment purposes.
