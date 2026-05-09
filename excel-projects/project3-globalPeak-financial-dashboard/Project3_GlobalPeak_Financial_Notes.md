# Project 3 — GlobalPeak Corp Financial KPI Dashboard

### Excel Data Analytics Portfolio | Anshul Raghuvanshi

---

## 📋 Table of Contents

1. [Project Overview](#1-project-overview)
2. [Business Case & User Story](#2-business-case--user-story)
3. [Dataset Details](#3-dataset-details)
4. [Workbook Structure](#4-workbook-structure)
5. [P&L Concepts Explained](#5-pl-concepts-explained)
6. [Formulas Explained](#6-formulas-explained)
7. [KPI Summary Analysis](#7-kpi-summary-analysis)
8. [PivotTable Analysis](#8-pivottable-analysis)
9. [Dashboard Design](#9-dashboard-design)
10. [Key Business Insights](#10-key-business-insights)
11. [Interview Q&A — 15 Questions](#11-interview-qa--15-questions)

---

## 1. Project Overview

| Field             | Details                                                                      |
| ----------------- | ---------------------------------------------------------------------------- |
| **Project Name**  | GlobalPeak Corp Financial KPI Dashboard                                      |
| **Tool Used**     | Microsoft Excel 365                                                          |
| **Dataset**       | Microsoft Financial Sample (Official)                                        |
| **Level**         | Advanced — Project 3 of 3                                                    |
| **Rows Analyzed** | 700 transactions                                                             |
| **Columns**       | 16 original + 5 helper = 21 total                                            |
| **Sheets Built**  | 6 (RAW_DATA, CLEANED_DATA, KPI_SUMMARY, PIVOT_ANALYSIS, DASHBOARD, INSIGHTS) |
| **Time Period**   | Sep 2013 — Dec 2014                                                          |

### What Was Built

A complete financial analytics workbook analyzing P&L performance across 5 segments, 5 countries, 6 products and 4 discount bands — with a Waterfall Chart, Timeline Slicer, and executive INSIGHTS sheet.

---

## 2. Business Case & User Story

### Business Context

**GlobalPeak Corp** (fictional) sells 6 products across 5 countries in 5 customer segments. The CFO needs a single-screen financial dashboard that updates when new monthly data is added — showing P&L breakdown, segment performance, and discount impact analysis.

### The Problem

```
❓ Which segment is actually profitable?
❓ How much revenue is lost to discounts?
❓ Which product generates most profit?
❓ How does discount level impact margins?
❓ Which country has best profit margin?
```

### User Story

> _"As the CFO, I need a one-page financial dashboard showing Revenue, Gross Margin, and Profit by segment and product — with discount impact analysis — so I can present to investors in 5 minutes with no manual prep work."_

### Solution Delivered

A 6-sheet Excel workbook with P&L analysis, Waterfall chart showing gross-to-net flow, Timeline Slicer for date filtering, and executive INSIGHTS sheet with strategic recommendations.

---

## 3. Dataset Details

| Field           | Value                                                                              |
| --------------- | ---------------------------------------------------------------------------------- |
| **Source**      | Microsoft Learn — Official Sample                                                  |
| **URL**         | https://docs.microsoft.com/en-us/power-bi/create-reports/sample-financial-download |
| **Rows**        | 700 transactions                                                                   |
| **Columns**     | 16                                                                                 |
| **Null Values** | 53 (Discount Band column only)                                                     |
| **Date Range**  | Sep 2013 — Dec 2014                                                                |

### Column Guide

| Column              | Description           | Type                        |
| ------------------- | --------------------- | --------------------------- |
| Segment             | Customer type         | Text (5 unique)             |
| Country             | Sales country         | Text (5 unique)             |
| Product             | Product name          | Text (6 unique)             |
| Discount Band       | Discount level        | Text (None/Low/Medium/High) |
| Units Sold          | Units per transaction | Number                      |
| Manufacturing Price | Cost per unit         | Currency                    |
| Sale Price          | Listed price per unit | Currency                    |
| Gross Sales         | Sale Price × Units    | Currency                    |
| Discounts           | Discount amount       | Currency                    |
| Sales (Net)         | Gross - Discounts     | Currency                    |
| COGS                | Mfg Price × Units     | Currency                    |
| Profit              | Net Sales - COGS      | Currency                    |
| Date                | Transaction date      | Date                        |
| Month Number        | 1-12                  | Number                      |
| Month Name          | January-December      | Text                        |
| Year                | 2013 or 2014          | Number                      |

### Important Data Notes

```
1. Sales column has leading space " Sales" — renamed to "Sales"
2. Discount Band has 53 nulls — treated as "No Discount"
3. 2013 = only 4 months (Sep-Dec) — NOT a full year!
   Direct YoY comparison would be misleading!
```

---

## 4. Workbook Structure

```
Project3_GlobalPeak_Financial_Dashboard.xlsx
│
├── 📋 RAW_DATA          (Gray tab)   — 700 rows × 16 cols
├── 🧹 CLEANED_DATA      (Blue tab)   — 700 rows × 21 cols
├── 📊 KPI_SUMMARY       (Red tab)    — 5 analysis sections
├── 🔄 PIVOT_ANALYSIS    (Green tab)  — 3 PivotTables + Timeline
├── 🎨 DASHBOARD         (Gold tab)   — 6 KPI cards + 4 charts
└── 💡 INSIGHTS          (Purple tab) — Executive report
```

---

## 5. P&L Concepts Explained

### What is P&L?

P&L (Profit & Loss) is the financial story of a business — how money came in and where it went.

### P&L Flow — GlobalPeak Corp

```
                        Amount           % of Net Sales
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Gross Sales          $127,931,599          107.8%
Less: Discounts       ($9,205,248)          (7.8%)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Net Sales            $118,726,350          100.0%  ← BASE
Less: COGS          ($101,832,648)         (85.8%)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Profit                $16,893,702           14.2%
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Key P&L Terms

| Term          | Definition               | Formula                  |
| ------------- | ------------------------ | ------------------------ |
| Gross Sales   | Revenue before discounts | Sale Price × Units       |
| Discounts     | Price reductions given   | Gross Sales × Discount % |
| Net Sales     | Actual revenue collected | Gross Sales - Discounts  |
| COGS          | Direct production cost   | Mfg Price × Units        |
| Profit        | Final bottom line        | Net Sales - COGS         |
| Profit Margin | Efficiency metric        | Profit / Net Sales       |

### Why Waterfall Chart?

```
Waterfall chart visualizes P&L flow:
Gross Sales → (minus Discounts) → Net Sales
→ (minus COGS) → Profit

Each bar shows how we went from $127.9M
to $16.9M — instantly understandable!
```

---

## 6. Formulas Explained

### 6.1 IF() — Profit*Margin*% Helper Column

```excel
=IF(J2=0, 0, L2/J2)
```

**Breakdown:**

```
J2 = Net Sales
L2 = Profit
L2/J2 = Profit Margin %
IF(J2=0,0,...) = Protect against #DIV/0! error
```

---

### 6.2 IF() — Discount_Pct Helper Column

```excel
=IF(H2=0, 0, I2/H2)
```

**Breakdown:**

```
H2 = Gross Sales
I2 = Discounts
I2/H2 = Discount % (what % of gross was discounted)
```

**Business use:**

```
High Discount % → Revenue leakage!
Row with 20% discount means:
$100 listed → only $80 collected!
```

---

### 6.3 Nested IF() — Sales_Category Helper Column

```excel
=IF(J2<10000,"Small",IF(J2<50000,"Medium",IF(J2<200000,"Large","Enterprise")))
```

**Categories:**

```
< $10,000   → Small
< $50,000   → Medium
< $200,000  → Large
≥ $200,000  → Enterprise (big ticket transactions!)
```

---

### 6.4 IF() — COGS_Pct Helper Column

```excel
=IF(J2=0, 0, K2/J2)
```

**Why important:**

```
COGS% + Profit% = 100% (always!)

Row check:
COGS% = 85.8%  +  Profit% = 14.2%  = 100% ✅

High COGS% = Thin margins
Low COGS%  = Healthy margins
```

---

### 6.5 IFERROR() — Profit_Flag Helper Column ← NEW!

```excel
=IFERROR(IF(L2>0,"Profitable",IF(L2=0,"Breakeven","Loss")),"Check Data")
```

**IFERROR syntax:**

```
=IFERROR(formula, value_if_error)
          │         │
          Try this  If any error occurs,
          formula   show this instead
```

**Why IFERROR:**

```
Without IFERROR:
If formula fails → #VALUE! or #DIV/0! shown

With IFERROR:
If formula fails → "Check Data" shown
Clean, professional output!
```

**Profit Flag results:**

```
L2 > 0 → "Profitable" ✅
L2 = 0 → "Breakeven"  ⚖️
L2 < 0 → "Loss"       ❌
```

---

### 6.6 % of Total ← NEW CONCEPT!

**Used in all KPI_SUMMARY sections:**

```excel
=C_row / $D$6
```

**Breakdown:**

```
C_row = Segment/Country/Product sales
$D$6  = Total Net Sales (ABSOLUTE reference!)

Government % = $52,504,261 / $118,726,350 = 44.22%

$D$6 is ABSOLUTE because:
→ Denominator (total) never changes
→ Only numerator (each segment) changes
```

**Why % of Total matters:**

```
Raw numbers: Government = $52.5M
             Small Business = $42.4M
             Difference = $10.1M

% of Total:  Government = 44.2%
             Small Business = 35.7%
             Gap = 8.5 percentage points

% makes comparison meaningful
regardless of total size!
```

---

### 6.7 Waterfall Chart — Negative Values

**Data table for Waterfall:**

```excel
Gross Sales  → =KPI_SUMMARY!D4    (Positive)
Discounts    → =-KPI_SUMMARY!D5   (NEGATIVE! ← minus sign)
Net Sales    → =KPI_SUMMARY!D6    (Positive — Set as Total)
COGS         → =-KPI_SUMMARY!D7   (NEGATIVE! ← minus sign)
Profit       → =KPI_SUMMARY!D8    (Positive — Set as Total)
```

**Why negative for Discounts and COGS?**

```
Waterfall chart logic:
Positive value → Bar goes UP   (adding value)
Negative value → Bar goes DOWN (reducing value)

Discounts reduce revenue → Must be negative!
COGS reduces profit     → Must be negative!

"Set as Total" for Net Sales and Profit:
→ These are subtotals, not increments
→ Bars start from zero (full height)
→ Shows the actual accumulated value
```

---

### 6.8 Timeline Slicer ← NEW!

**What it is:**

```
Timeline Slicer = Date-based visual filter
Click/drag months → PivotTable filters instantly!
```

**How to add:**

```
1. PivotTable pe click
2. PivotTable Analyze → Insert Timeline
3. Date column select → OK
4. Timeline appears — drag to position
```

**Timeline levels:**

```
YEARS → QUARTERS → MONTHS → DAYS
```

**Use case:**

```
"Show me only Q4 2014 performance"
→ Drag timeline to Oct-Dec 2014
→ PivotTable updates instantly!
→ No formula needed!
```

---

## 7. KPI Summary Analysis

### Section 1 — Overall Financial KPIs

| KPI             | Value        | Formula             |
| --------------- | ------------ | ------------------- |
| Gross Sales     | $127,931,599 | `=SUM(H2:H701)`     |
| Total Discounts | $9,205,248   | `=SUM(I2:I701)`     |
| Net Sales       | $118,726,350 | `=SUM(J2:J701)`     |
| Total COGS      | $101,832,648 | `=SUM(K2:K701)`     |
| Total Profit    | $16,893,702  | `=SUM(L2:L701)`     |
| Profit Margin   | 14.23%       | `=IF(D6=0,0,D8/D6)` |
| Total Units     | 1,125,806    | `=SUM(E2:E701)`     |

### Section 2 — By Segment

| Segment          | Net Sales       | % Total    | Profit        | Margin        |
| ---------------- | --------------- | ---------- | ------------- | ------------- |
| Government       | $52,504,261     | 44.22%     | $11,388,173   | 21.69% ✅     |
| Small Business   | $42,427,919     | 35.74%     | $4,143,169    | 9.77% ⚠️      |
| **Enterprise**   | **$19,611,694** | **16.52%** | **-$614,546** | **-3.13%** ❌ |
| Midmarket        | $2,381,883      | 2.01%      | $660,103      | 27.71% ✅     |
| Channel Partners | $1,800,594      | 1.52%      | $1,316,803    | 73.13% 🏆     |

### Section 3 — By Country

| Country     | Net Sales       | % Total    | Profit         | Margin        |
| ----------- | --------------- | ---------- | -------------- | ------------- |
| Canada      | $24,887,655     | 20.96%     | $3,529,229     | 14.18%        |
| **Germany** | **$23,505,341** | **19.80%** | **$3,680,389** | **15.66%** 🏆 |
| France      | $24,354,172     | 20.51%     | $3,781,021     | 15.53%        |
| Mexico      | $20,949,352     | 17.65%     | $2,907,523     | 13.88%        |
| USA         | $25,029,830     | 21.08%     | $2,995,541     | 11.97% ⚠️     |

### Section 4 — By Product

| Product   | Net Sales       | % Total    | Profit         | Margin        |
| --------- | --------------- | ---------- | -------------- | ------------- |
| **Paseo** | **$33,011,144** | **27.80%** | **$4,797,438** | **14.53%** 🏆 |
| VTT       | $20,511,921     | 17.28%     | $3,034,608     | 14.79%        |
| Velo      | $18,250,059     | 15.37%     | $2,305,992     | 12.64%        |
| Amarilla  | $17,747,116     | 14.95%     | $2,814,104     | **15.86%** 🏆 |
| Montana   | $15,390,802     | 12.96%     | $2,114,755     | 13.74%        |
| Carretera | $13,815,308     | 11.64%     | $1,826,805     | 13.22%        |

### Section 5 — By Year

| Year | Net Sales   | % Total | Profit      | Margin | Note              |
| ---- | ----------- | ------- | ----------- | ------ | ----------------- |
| 2013 | $26,415,256 | 22.25%  | $3,878,465  | 14.68% | ⚠️ 4 months only! |
| 2014 | $92,311,095 | 77.75%  | $13,015,238 | 14.10% | Full year         |

---

## 8. PivotTable Analysis

### PivotTable 1 — Segment × Year Matrix

```
ROWS: Segment | COLUMNS: Year | VALUES: Net Sales
Grand Total: $118,726,350 ✅
```

### PivotTable 2 — Product × Country Profit Matrix

```
ROWS: Product | COLUMNS: Country | VALUES: Profit
Grand Total: $16,893,702 ✅
Key: Paseo profitable in ALL 5 countries!
```

### PivotTable 3 — Discount Band Analysis + Timeline Slicer

| Discount Band | Net Sales   | Profit     | Margin    |
| ------------- | ----------- | ---------- | --------- |
| None          | $7,943,654  | $1,736,455 | 21.86% 🟢 |
| Low           | $34,629,779 | $6,188,858 | 17.87% 🟢 |
| Medium        | $38,780,431 | $5,579,523 | 14.39% 🟠 |
| High          | $37,372,487 | $3,388,867 | 9.07% 🔴  |

**Timeline Slicer:** Connected to Date column — filter by months/quarters/years interactively!

---

## 9. Dashboard Design

### KPI Cards

| Card          | Formula            | Color  |
| ------------- | ------------------ | ------ |
| Gross Sales   | `=KPI_SUMMARY!D4`  | Blue   |
| Net Sales     | `=KPI_SUMMARY!D6`  | Green  |
| Total Profit  | `=KPI_SUMMARY!D8`  | Red    |
| Profit Margin | `=KPI_SUMMARY!D9`  | Orange |
| Total COGS    | `=KPI_SUMMARY!D7`  | Purple |
| Units Sold    | `=KPI_SUMMARY!D10` | Teal   |

### Charts

| Chart             | Type           | Key Insight                     |
| ----------------- | -------------- | ------------------------------- |
| P&L Waterfall     | Waterfall      | Gross→Disc→Net→COGS→Profit flow |
| Sales by Segment  | Column         | Government dominates 44.2%      |
| Profit by Product | Horizontal Bar | Paseo #1 at $5M                 |
| Sales by Year     | Column         | 2014 = 3.5x 2013 (4 months!)    |

### Waterfall Chart — Why Unique?

```
Most dashboards show final numbers.
Waterfall shows the JOURNEY:
$127.9M → -$9.2M → $118.7M → -$101.8M → $16.9M

CFO can see exactly where money is going!
This is standard in financial presentations.
```

---

## 10. Key Business Insights

### 🔴 Critical Findings

```
1. Enterprise Segment = LOSS!
   $19.6M sales → -$614,546 profit
   -3.13% margin → Company LOSING money!
   Action: Immediate pricing review needed

2. COGS = 85.8% of Net Sales
   $101.8M of $118.7M goes to production!
   Only 14.2% left as profit
   Action: Negotiate raw material costs

3. High Discount = Half the Margin
   High band:  9.07%  ← Nearly half!
   Low band:  17.87%  ← Healthy!
   Action: Cap high discount approvals

4. 2013 only 4 months data
   Direct YoY comparison misleading!
   Action: Need Sep-Dec 2013 vs 2014 comparison
```

### 🟠 Warning Signals

```
1. Small Business margin only 9.77%
   35.7% of revenue but low profitability!

2. USA lowest margin (11.97%)
   Despite being biggest market ($25M)!

3. Velo lowest product margin (12.64%)
   Room for price increase?
```

### 🟢 Positive Findings

```
1. Channel Partners = 73.13% margin!
   Smallest segment but MOST efficient!
   Only $1.8M sales but $1.3M profit!

2. Government = 44.2% revenue + 21.69% margin
   Best combination of size AND profitability!

3. Paseo = Star product
   27.8% of all revenue + $4.8M profit
   Profitable in ALL 5 countries!

4. Germany = Best country margin (15.66%)
   Consistent performer across all products!
```

### 💡 Strategic Recommendations

| Priority  | Action                    | Expected Impact         |
| --------- | ------------------------- | ----------------------- |
| 🔴 HIGH   | Fix Enterprise pricing    | Stop -$614K losses      |
| 🔴 HIGH   | Cap High discount band    | Margin +5-8%            |
| 🔴 HIGH   | Reduce COGS               | Every 1% = $1M+ profit  |
| 🟠 MEDIUM | Expand Government segment | Best ROI segment        |
| 🟠 MEDIUM | Replicate Germany in USA  | USA margin improvement  |
| 🟢 LOW    | Push Paseo aggressively   | Revenue + profit growth |

---

## 11. Interview Q&A — 15 Questions

---

### Q1. What is a P&L statement and what are its key components?

**Answer:**
P&L (Profit & Loss) shows financial performance over a period. Key components:

- **Gross Sales**: Total revenue before deductions
- **Discounts**: Price reductions given to customers
- **Net Sales**: Actual revenue (Gross - Discounts) — the base for all % calculations
- **COGS**: Direct cost of producing goods sold
- **Profit**: Final bottom line (Net Sales - COGS)
- **Profit Margin**: Efficiency ratio (Profit / Net Sales)

---

### Q2. What is a Waterfall chart and when would you use it?

**Answer:**
A Waterfall chart visualizes how an initial value increases or decreases through intermediate steps to reach a final value. Each bar represents a positive (blue) or negative (red) contribution.

Use when: Showing P&L breakdown, budget variance analysis, or any sequential financial flow. In this project, it shows the journey from $127.9M Gross Sales to $16.9M Profit — CFOs and executives can instantly see where money is going.

---

### Q3. Why did you use negative values for Discounts and COGS in the Waterfall chart?

**Answer:**
Waterfall charts interpret positive values as upward bars (adding value) and negative values as downward bars (reducing value). Since Discounts and COGS reduce the financial position, they must be negative so the chart correctly shows them as decreasing bars. Net Sales and Profit are marked as "Set as Total" so they display as full-height reference bars.

---

### Q4. What is IFERROR() and why is it better than IF() for error handling?

**Answer:**

```
IF():      =IF(A1=0, 0, B1/A1)  — handles one specific error
IFERROR(): =IFERROR(B1/A1, 0)   — handles ANY error type
```

IFERROR is cleaner because it catches all error types (#DIV/0!, #VALUE!, #REF!, #N/A) in one formula. It's especially useful when wrapping complex formulas like VLOOKUP or nested calculations where multiple error types could occur.

---

### Q5. What is % of Total and why is it more useful than raw numbers?

**Answer:**
% of Total = Individual value / Grand Total

Raw numbers show absolute size. % of Total shows relative contribution regardless of scale:

```
Government: $52.5M = 44.2% of total
Enterprise: $19.6M = 16.5% of total
```

If total grows next year, % shows whether each segment grew proportionally or not. Essential for portfolio analysis and market share tracking.

---

### Q6. What is a Timeline Slicer and how is it different from a regular Slicer?

**Answer:**

- **Regular Slicer**: Filters by category (text values like Segment, Country)
- **Timeline Slicer**: Filters by DATE — shows a visual calendar/timeline

Timeline Slicer allows selecting specific months, quarters, or years by clicking/dragging. In this project, it's connected to the Discount Band PivotTable — filtering to Q4 2014 shows performance in that specific period without writing any formulas.

---

### Q7. Why is 2013 vs 2014 comparison potentially misleading in this dataset?

**Answer:**
2013 data contains only 4 months (September to December). Comparing $26.4M (2013) directly to $92.3M (2014) shows 3.5x growth — but this is primarily because 2014 has 12 months of data. A fair comparison would be September-December 2013 vs September-December 2014. I addressed this by adding a note directly on the chart to prevent misinterpretation.

---

### Q8. What does COGS% tell you about a business?

**Answer:**
COGS% = COGS / Net Sales shows what percentage of revenue goes to direct production costs.

In GlobalPeak: COGS% = 85.8% — very high! Means only 14.2% remains as profit. Lower COGS% = higher margin. If COGS% drops from 85.8% to 83.8%, that's a 2% improvement = approximately $2.3M additional profit on the same revenue.

---

### Q9. Enterprise segment has $19.6M in sales but is making a loss. How would you investigate this?

**Answer:**
I would analyze:

1. Discount Band distribution for Enterprise — are they getting excessive discounts?
2. Product mix — are they buying low-margin products?
3. COGS structure — are production costs higher for Enterprise-targeted products?
4. Country breakdown — is the loss concentrated in specific markets?

In this dataset, Enterprise likely receives heavy discounts (High discount band) which erodes the 14% average margin into negative territory.

---

### Q10. Why does Channel Partners have 73% margin despite lowest revenue?

**Answer:**
Channel Partners likely:

1. Receive minimal discounts (Low/No discount band)
2. Buy high-margin products (possibly Amarilla with 15.86% margin)
3. Order in efficient quantities reducing per-unit costs

This illustrates that revenue size ≠ profitability. A $1.8M segment with 73% margin ($1.3M profit) can be more valuable than a $19.6M segment with negative margin.

---

### Q11. How would you explain the difference between Gross Sales and Net Sales to a non-technical stakeholder?

**Answer:**
"Imagine you list a product at $100 (Gross Sales). You give a 10% discount to a customer, so they pay $90 (Net Sales). The $10 difference is the Discount. Net Sales is the actual money that comes into the business — that's why all our margin calculations use Net Sales as the base, not Gross Sales."

---

### Q12. What is the significance of 'Set as Total' in a Waterfall chart?

**Answer:**
In Excel's Waterfall chart, each bar by default represents an increment or decrement from the previous bar (floating). "Set as Total" makes a bar start from zero and show the accumulated value — it becomes a reference/subtotal bar.

In our P&L waterfall:

- Net Sales = Total after discounts → Set as Total (shows $118.7M from zero)
- Profit = Final result → Set as Total (shows $16.9M from zero)

Without this setting, these bars would float at incorrect positions.

---

### Q13. How does discount level impact profit margin in this dataset?

**Answer:**
Clear inverse relationship:

```
No Discount → 21.86% margin (best!)
Low         → 17.87% margin
Medium      → 14.39% margin
High        → 9.07%  margin (worst!)
```

Every discount tier reduces margin by approximately 4-5 percentage points. High discount customers generate only 9 cents of profit per dollar of revenue vs 22 cents for non-discounted customers. The CFO recommendation: limit High discount approvals.

---

### Q14. What is the DRY principle and how did you apply it in this project?

**Answer:**
DRY = "Don't Repeat Yourself" — avoid recalculating the same thing multiple times.

Applied in:

```
Profit Margin formula: =IF(D6=0,0,D8/D6)
→ Uses already-calculated D6 (Net Sales) and D8 (Profit)
→ Does NOT recalculate from raw data again
→ If underlying data changes, both update together
→ Faster, more maintainable, less error-prone
```

---

### Q15. If a new month of data is added, how would this dashboard update?

**Answer:**

1. Paste new rows in RAW_DATA (below row 701)
2. Extend CLEANED_DATA helper formulas for new rows
3. KPI_SUMMARY SUMIF formulas auto-expand (using full column references)
4. Refresh 3 PivotTables (right-click → Refresh All)
5. Dashboard KPI cards auto-update (linked to KPI_SUMMARY)
6. Timeline Slicer automatically includes new dates
7. INSIGHTS Live KPI section auto-updates

This demonstrates the **scalable pipeline design** — one data refresh cascades through the entire workbook!

---

## Excel Skills — Complete Project 3 Summary

| Skill                              | Used Where                      |
| ---------------------------------- | ------------------------------- |
| IFERROR()                          | Profit_Flag helper column       |
| % of Total                         | All KPI_SUMMARY sections        |
| Waterfall Chart                    | Dashboard — P&L visualization   |
| Timeline Slicer                    | PIVOT_ANALYSIS — date filtering |
| Nested IF                          | Sales_Category classification   |
| SUMIF                              | All KPI sections                |
| Negative values in charts          | Waterfall chart design          |
| "Set as Total"                     | Waterfall Net Sales + Profit    |
| Custom number format ($#,##0,,"M") | Y-axis labels                   |
| Text Box in chart                  | 2013 data note                  |
| Cross-sheet formulas               | Dashboard → KPI_SUMMARY         |
| Data Integrity checks              | All section totals verified     |

---
