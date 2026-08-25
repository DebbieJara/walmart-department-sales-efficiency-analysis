# Walmart Department Sales & Efficiency Analysis

![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=flat&logo=google-sheets&logoColor=white)

**Business question:** Walmart operates hundreds of departments across stores of different sizes. Which departments are actually driving revenue, and which ones are occupying valuable floor space without delivering proportional results?

## Context

This analysis was built to answer that question using Walmart's 2012 weekly sales data.

## Process

Built a full analytical pipeline in Google Sheets, from raw data to executive dashboard: cleaned the data, joined department and store catalogues, validated data quality, defined KPIs, and built an interactive dashboard that makes the findings immediately actionable.

## Key findings

Two metrics told the real story:

- **Participation %** showed which departments contributed most to total revenue, helping prioritize commercial strategy.
- **Sales per m²** exposed which departments were truly efficient versus those that looked strong on paper but underperformed relative to their store footprint.

Data quality checks confirmed 6,435 records without a matched department, 27 negative sales values, and no missing store size data. All checks were handled before any analysis was run. Notably, department code 16, representing 5.27% of 2012 sales, has no matching entry in the department catalogue: a data governance gap flagged for the data team rather than silently excluded.

## Dashboard

![Walmart department sales and efficiency dashboard](images/department-sales-dashboard.png)

Interactive dashboard filterable by department, showing sales per m², participation %, and sales volatility (coefficient of variation) side by side.

## Technical details

### File structure

| Sheet | Description | Type |
|---|---|---|
| raw_ventas | Original weekly sales data by store and department | Raw Data |
| raw_departamento | Department catalogue with names | Lookup |
| raw_tiendas | Store catalogue with type (A/B) and size in m² | Lookup |
| clean_ventas | Cleaned data with catalogue joins, standardised week, and department name | Clean Data |
| Pivot | Dynamic tables with aggregated metrics by department | Pivot Tables |
| Dashboard | Interactive widget to filter by department, showing KPIs, charts and visualisations | Dashboard |
| Resumen | Synthesis of findings, insights and business implications | Analytical Summary |

### KPIs & formulas

| KPI | Description | Formula | Interpretation |
|---|---|---|---|
| Sales per m² | Sales adjusted by store size | Total Sales / Store Size | Higher values indicate greater efficiency per square metre |
| Participation % | Each department's proportion of total 2012 sales | Dept Sales / Total Sales | High values = greater contribution to total revenue |

### Data quality checks

| Check | Formula | Result |
|---|---|---|
| Records without a matched department | `=CONTAR.SI(clean_ventas!I:I,"No existe")` | 6,435 |
| Negative or null sales | `=COUNTIF(clean_ventas!D:D,"<0")` | 27 |
| Store sizes with value 0 or blank | `=COUNTIF(raw_tiendas!C2:C46,0)+COUNTBLANK(raw_tiendas!C2:C46)` | 0 |

## Tools

Google Sheets · VLOOKUP · Pivot Tables · COUNTIF · Dashboard
