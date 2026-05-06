# Project 1 — FreshMart Retail Sales Dashboard

### Excel Data Analytics Portfolio | Anshul Raghuvanshi

---

## 📋 Table of Contents

1. [Project Overview](#project-overview)
2. [Business Case & User Story](#business-case)
3. [Dataset Details](#dataset-details)
4. [Workbook Structure](#workbook-structure)
5. [Formulas Explained](#formulas-explained)
6. [KPI Summary Analysis](#kpi-summary-analysis)
7. [PivotTable Analysis](#pivottable-analysis)
8. [Dashboard Design](#dashboard-design)
9. [Key Business Insights](#key-business-insights)
10. [Interview Q&A — 15 Questions](#interview-qa)

---

## 1. Project Overview

| Field             | Details                                                            |
| ----------------- | ------------------------------------------------------------------ |
| **Project Name**  | FreshMart Retail Sales Performance Dashboard                       |
| **Tool Used**     | Microsoft Excel 365                                                |
| **Dataset**       | Sample Superstore (Kaggle / Tableau Public)                        |
| **Level**         | Basic — Project 1 of 3                                             |
| **Time Period**   | 2014 – 2017 (4 years)                                              |
| **Rows Analyzed** | 9,994 order line items                                             |
| **Sheets Built**  | 5 (RAW_DATA, CLEANED_DATA, KPI_SUMMARY, PIVOT_ANALYSIS, DASHBOARD) |

### What Was Built

A complete end-to-end retail sales analytics workbook that transforms 9,994 raw order records into a clean, interactive dashboard — showing regional performance, category profitability, yearly trends and customer segment analysis.

---

## 2. Business Case & User Story

### Business Context

**FreshMart Retail** (fictional) operates across 4 regions (East, West, Central, South) selling products across 3 categories: Furniture, Office Supplies, and Technology. The company has 4 years of sales data (2014–2017) across 3 customer segments: Consumer, Corporate, and Home Office.

### The Problem

The Regional Sales Manager was drowning in 9,994 rows of raw data with no way to quickly answer key business questions:

- Which region is performing best?
- Which product category is actually profitable?
- Is the business growing year over year?
- Which customer segment drives the most revenue?

### User Story

> _"As a Regional Sales Manager, I want to see monthly and yearly sales performance by region, product category, and customer segment — so I can identify underperforming areas and make data-driven decisions before the quarter ends."_

### Solution Delivered

A 5-sheet Excel workbook with:

- Automated KPI calculations (SUMIF, COUNTIF)
- Interactive PivotTables for ad-hoc analysis
- A professional dashboard with 5 KPI cards and 4 charts

---

## 3. Dataset Details

| Field             | Value                                                             |
| ----------------- | ----------------------------------------------------------------- |
| **Source**        | Kaggle — Sample Superstore Dataset                                |
| **Download URL**  | https://www.kaggle.com/datasets/vivek468/superstore-dataset-final |
| **File Format**   | .csv                                                              |
| **Total Rows**    | 9,994                                                             |
| **Total Columns** | 21                                                                |
| **Date Range**    | January 2014 — December 2017                                      |
| **Encoding**      | Latin-1                                                           |

### Key Columns Used

| Column        | Data Type | Description                                            |
| ------------- | --------- | ------------------------------------------------------ |
| Order ID      | Text      | Unique order identifier                                |
| Order Date    | Date      | When customer placed order                             |
| Ship Date     | Date      | When order was shipped                                 |
| Ship Mode     | Text      | Second Class / Standard Class / First Class / Same Day |
| Customer Name | Text      | Customer full name                                     |
| Segment       | Text      | Consumer / Corporate / Home Office                     |
| Region        | Text      | East / West / Central / South                          |
| Category      | Text      | Furniture / Office Supplies / Technology               |
| Sub-Category  | Text      | 17 unique sub-categories                               |
| Sales         | Number    | Revenue from order (USD)                               |
| Quantity      | Integer   | Units ordered                                          |
| Discount      | Decimal   | Discount rate (0 to 1)                                 |
| Profit        | Number    | Profit/Loss from order (can be negative)               |

---

## 4. Workbook Structure

```
Project1_FreshMart_Dashboard.xlsx
│
├── 📋 RAW_DATA          (Gray tab)
│   └── Original 9,994 rows — never modified
│
├── 🧹 CLEANED_DATA      (Blue tab)
│   └── All 21 original columns + 5 helper columns
│
├── 📊 KPI_SUMMARY       (Red tab)
│   └── 5 analysis sections using SUMIF/COUNTIF formulas
│
├── 🔄 PIVOT_ANALYSIS    (Green tab)
│   └── 3 PivotTables for multi-dimensional analysis
│
└── 🎨 DASHBOARD         (Gold tab)
    └── 5 KPI Cards + 4 Charts
```

### Golden Rule Applied

> **Raw data is NEVER modified.** All analysis is done on copies and summary sheets. This ensures the source of truth is always preserved.

---

## 5. Formulas Explained

### 5.1 YEAR() — Extract Year from Date

**Sheet:** CLEANED_DATA | **Column:** V

```excel
=YEAR(C2)
```

**How it works:**

- `C2` = Order Date cell containing a date like `11/08/2016`
- `YEAR()` extracts only the year number → returns `2016`
- Excel stores dates as serial numbers internally, so YEAR() reads that number and returns the year component

**Why needed:**

- SUMIF requires an exact match criteria
- We cannot SUMIF on full dates to get yearly totals
- By extracting year into its own column, we can do `=SUMIF(V:V, 2016, R:R)` to get 2016 sales

**Result Range:** 2014, 2015, 2016, or 2017

---

### 5.2 TEXT() — Format Date as Label

**Sheet:** CLEANED_DATA | **Column:** W

```excel
=TEXT(C2,"MMM-YY")
```

**How it works:**

- `C2` = Order Date
- `"MMM-YY"` = format code:
  - `MMM` = 3-letter month abbreviation (Jan, Feb, Mar...)
  - `-` = literal dash character
  - `YY` = 2-digit year (14, 15, 16, 17)
- Returns a text string like `"Nov-16"`

**Format Code Reference:**

| Code   | Output       | Example  |
| ------ | ------------ | -------- |
| `MMM`  | Short month  | Nov      |
| `MMMM` | Full month   | November |
| `MM`   | Month number | 11       |
| `YY`   | 2-digit year | 16       |
| `YYYY` | 4-digit year | 2016     |
| `DD`   | Day number   | 08       |

**Important:** TEXT() returns TEXT, not a number. This means you cannot do arithmetic on it. Use YEAR() when you need numeric calculations.

---

### 5.3 IF() — Conditional Logic (Profit Margin)

**Sheet:** CLEANED_DATA | **Column:** X

```excel
=IF(R2=0, 0, U2/R2)
```

**How it works:**

```
IF(logical_test, value_if_true, value_if_false)
   │              │               │
   R2=0           0               U2/R2
   "Is Sales=0?"  "Return 0"      "Calculate Profit/Sales"
```

**Why the IF guard is needed:**

- `U2/R2` = Profit ÷ Sales = Margin %
- If Sales (R2) = 0, this becomes `n/0` → Excel shows `#DIV/0!` error
- The IF catches this case and returns 0 instead of an error
- This is called **defensive formula writing** — always protect against division by zero

**Format applied:** Percentage with 2 decimal places → `0.00%`

---

### 5.4 Nested IF() — Sales Band Categorization

**Sheet:** CLEANED_DATA | **Column:** Y

```excel
=IF(R2>=1000,"High", IF(R2>=100,"Medium","Low"))
```

**How it works:**

```
Step 1: Is Sales >= $1000?
        YES → "High" (stop here)
        NO  → go to Step 2

Step 2: Is Sales >= $100?
        YES → "Medium" (stop here)
        NO  → "Low" (default)
```

**Critical Rule — Order Matters:**

```excel
❌ WRONG:  =IF(R2>=100,"Medium", IF(R2>=1000,"High","Low"))
           A $2000 order hits >=100 first → "Medium" WRONG!

✅ CORRECT: =IF(R2>=1000,"High", IF(R2>=100,"Medium","Low"))
            A $2000 order hits >=1000 first → "High" CORRECT!
```

**Always write conditions from most restrictive to least restrictive.**

**Results found:**

- High (≥$1000): 468 orders (4.7%)
- Medium (≥$100): 3,300 orders (33.0%)
- Low (<$100): 6,226 orders (62.3%)

---

### 5.5 Date Subtraction — Days to Ship

**Sheet:** CLEANED_DATA | **Column:** Z

```excel
=D2-C2
```

**How it works:**

- Excel stores all dates as serial numbers since January 1, 1900
  - Example: `11/08/2016` = serial number `42682`
  - Example: `11/11/2016` = serial number `42685`
- Subtracting two date serial numbers gives the difference in days
  - `42685 - 42682 = 3 days`
- No special function needed — simple subtraction works!

**Important:** After the formula, format the column as **Number** (not Date). Otherwise Excel shows the result as a date like `1/3/1900` instead of `3`.

---

### 5.6 SUM() — Total Aggregation

**Sheet:** KPI_SUMMARY

```excel
=SUM(CLEANED_DATA!R:R)
```

**Cross-sheet reference syntax:**

```
=SUM( CLEANED_DATA ! R:R )
       │              │
       Sheet name     Column R (entire column)
       followed by !  = Sales column
```

**The `!` (exclamation mark)** is Excel's way of referencing another sheet. Format: `SheetName!CellReference`

---

### 5.7 SUMIF() — Conditional Sum

**Sheet:** KPI_SUMMARY

```excel
=SUMIF(CLEANED_DATA!M:M, "West", CLEANED_DATA!R:R)
```

**Syntax:**

```
=SUMIF(range, criteria, sum_range)
        │       │         │
        M:M     "West"    R:R
        Where   What to   What to
        to look look for  add up
```

**How it works — row by row:**

```
Row 2:  M2="West" ✅ → Add R2 ($261.96)
Row 3:  M3="East" ❌ → Skip
Row 4:  M4="West" ✅ → Add R4 ($14.62)
...
Final: Sum of all West rows = $725,457.82
```

**Criteria types:**

| Criteria Type | Example        | Quotes Needed? |
| ------------- | -------------- | -------------- |
| Text          | "West", "East" | YES — always   |
| Number        | 2014, 2016     | NO             |
| With operator | ">100", "<=50" | YES            |

---

### 5.8 COUNTIF() — Conditional Count

**Sheet:** KPI_SUMMARY

```excel
=COUNTIF(CLEANED_DATA!M:M, "West")
```

**Syntax:**

```
=COUNTIF(range, criteria)
          │       │
          M:M     "West"
          Where   What to
          to look count
```

**Difference from SUMIF:**

- `SUMIF` → adds values from a separate column
- `COUNTIF` → only counts matching rows (no sum_range needed)
- Use SUMIF when you want totals, use COUNTIF when you want counts

---

### 5.9 COUNTA() — Count Non-Empty Cells

**Sheet:** KPI_SUMMARY

```excel
=COUNTA(CLEANED_DATA!B2:B9995)
```

**Why COUNTA not COUNT:**

- `COUNT` → counts only numeric values
- `COUNTA` → counts ALL non-empty cells (text, numbers, dates)
- Order ID column (B) contains text like "CA-2016-152156"
- `COUNT(B:B)` would return 0 (no numbers!)
- `COUNTA(B2:B9995)` returns 9,994 (all order IDs)

**Why B2 not B1:**

- B1 contains "Order ID" (the header)
- Starting from B2 excludes the header from the count

---

## 6. KPI Summary Analysis

### Section 1 — Overall Business KPIs

| KPI                   | Value         | Formula                          |
| --------------------- | ------------- | -------------------------------- |
| Total Sales Revenue   | $2,297,200.86 | `=SUM(CLEANED_DATA!R:R)`         |
| Total Profit Earned   | $286,397.02   | `=SUM(CLEANED_DATA!U:U)`         |
| Total No. of Orders   | 9,994         | `=COUNTA(CLEANED_DATA!B2:B9995)` |
| Overall Profit Margin | 12.47%        | `=SUM(U:U)/SUM(R:R)`             |
| Average Order Value   | $229.86       | `=SUM(R:R)/COUNTA(B2:B9995)`     |
| Total Units Sold      | 37,873        | `=SUM(CLEANED_DATA!S:S)`         |

### Section 2 — Sales by Region

| Region   | Total Sales     | Total Profit    | Orders    | Margin     |
| -------- | --------------- | --------------- | --------- | ---------- |
| East     | $678,781.24     | $91,522.78      | 2,848     | 13.48%     |
| **West** | **$725,457.82** | **$108,418.45** | **3,203** | **14.94%** |
| Central  | $501,239.89     | $39,706.36      | 2,323     | 7.92%      |
| South    | $391,721.91     | $46,749.43      | 1,620     | 11.93%     |

### Section 3 — Sales by Category

| Category        | Total Sales     | Total Profit    | Orders | Margin       |
| --------------- | --------------- | --------------- | ------ | ------------ |
| Furniture       | $741,999.80     | $18,451.27      | 2,121  | **2.49%** ⚠️ |
| Office Supplies | $719,047.03     | $122,490.80     | 6,026  | 17.04%       |
| **Technology**  | **$836,154.03** | **$145,454.95** | 1,847  | **17.40%**   |

### Section 4 — Sales by Segment

| Segment      | Total Sales       | Total Profit | Orders | Margin     |
| ------------ | ----------------- | ------------ | ------ | ---------- |
| **Consumer** | **$1,161,401.34** | $134,119.21  | 5,191  | 11.55%     |
| Corporate    | $706,146.37       | $91,979.13   | 3,020  | 13.03%     |
| Home Office  | $429,653.15       | $60,298.68   | 1,783  | **14.03%** |

### Section 5 — Sales by Year

| Year     | Total Sales     | Total Profit   | Orders    | Margin |
| -------- | --------------- | -------------- | --------- | ------ |
| 2014     | $484,247.50     | $49,543.97     | 1,993     | 10.23% |
| 2015     | $470,532.51     | $61,618.60     | 2,102     | 13.10% |
| 2016     | $609,205.60     | $81,795.17     | 2,587     | 13.43% |
| **2017** | **$733,215.26** | **$93,439.27** | **3,312** | 12.74% |

---

## 7. PivotTable Analysis

### PivotTable 1 — Region × Year Sales Matrix

| Region  | 2014     | 2015     | 2016     | 2017     | Total    |
| ------- | -------- | -------- | -------- | -------- | -------- |
| Central | $103,838 | $102,874 | $147,429 | $147,098 | $501,240 |
| East    | $128,680 | $156,332 | $180,686 | $213,083 | $678,781 |
| South   | $103,846 | $71,360  | $93,610  | $122,906 | $391,722 |
| West    | $147,883 | $139,966 | $187,480 | $250,128 | $725,458 |

**Key Observation:** East region shows strongest growth — $128K (2014) to $213K (2017) = **+65.6% growth!**

### PivotTable 2 — Category × Segment Breakdown

| Category        | Consumer | Corporate | Home Office | Total    |
| --------------- | -------- | --------- | ----------- | -------- |
| Furniture       | $391,049 | $229,020  | $121,931    | $742,000 |
| Office Supplies | $363,952 | $230,676  | $124,418    | $719,047 |
| Technology      | $406,400 | $246,450  | $183,304    | $836,154 |

**Key Observation:** Technology dominates in ALL segments — especially Home Office ($183K = highest margin combo)

### PivotTable 3 — Sub-Category Ranking

| Rank | Sub-Category | Sales    | Profit       | Status        |
| ---- | ------------ | -------- | ------------ | ------------- |
| 1    | Phones       | $330,007 | $44,516      | ✅ Profitable |
| 2    | Chairs       | $328,449 | $26,590      | ✅ Profitable |
| 3    | Storage      | $223,844 | $21,279      | ✅ Profitable |
| 4    | Tables       | $206,966 | **-$17,725** | ❌ LOSS       |
| 5    | Binders      | $203,413 | $30,222      | ✅ Profitable |
| ...  | ...          | ...      | ...          | ...           |
| -    | Bookcases    | $114,880 | **-$3,472**  | ❌ LOSS       |
| -    | Supplies     | $46,674  | **-$1,189**  | ❌ LOSS       |

**⚠️ Alert: 3 sub-categories operating at a LOSS:**

- Tables, Bookcases, Supplies — all in Furniture category
- This explains Furniture's extremely low 2.49% margin

---

## 8. Dashboard Design

### Design Principles Applied

1. **No Gridlines** — Hidden for clean, app-like appearance
2. **Color Coding** — Each KPI has a distinct color identity
3. **2×2 Chart Layout** — Balanced visual hierarchy
4. **Cross-sheet Linking** — KPI cards linked to KPI_SUMMARY (auto-update)
5. **Minimal Text** — Charts speak for themselves

### KPI Card Design

| Card            | Color  | Formula           |
| --------------- | ------ | ----------------- |
| Total Sales     | Green  | `=KPI_SUMMARY!D4` |
| Total Profit    | Blue   | `=KPI_SUMMARY!D5` |
| Profit Margin   | Orange | `=KPI_SUMMARY!D7` |
| Total Orders    | Teal   | `=KPI_SUMMARY!D6` |
| Avg Order Value | Red    | `=KPI_SUMMARY!D8` |

### Charts Used

| Chart              | Type              | Data Source                  | Purpose                      |
| ------------------ | ----------------- | ---------------------------- | ---------------------------- |
| Sales by Region    | Clustered Column  | KPI_SUMMARY Region section   | Compare regional performance |
| Yearly Sales Trend | Line with Markers | KPI_SUMMARY Year section     | Show growth over time        |
| Sales by Category  | Doughnut          | KPI_SUMMARY Category section | Show category proportion     |
| Profit by Region   | Horizontal Bar    | KPI_SUMMARY Region section   | Compare profitability        |

---

## 9. Key Business Insights

### 🏆 Insight 1 — West is the Best Region

```
West Region: $725,458 sales | 14.94% margin | 3,203 orders
→ Highest revenue AND highest margin
→ Strategy: Replicate West's approach in other regions
```

### ⚠️ Insight 2 — Central Region is a Concern

```
Central Region: $501,239 sales | ONLY 7.92% margin
→ Lowest margin among all regions
→ Reason: Likely over-discounting
→ Action: Review discount policy in Central region
```

### 🔴 Insight 3 — Furniture is Bleeding Money

```
Furniture Category: $741,999 sales | ONLY 2.49% margin
Sub-categories in LOSS:
  - Tables:    -$17,725 loss
  - Bookcases: -$3,472 loss
  - Supplies:  -$1,189 loss
→ Action: Reprice Furniture or reduce discounts
```

### 💡 Insight 4 — Technology = Sweet Spot

```
Technology: $836,154 sales | 17.40% margin | 1,847 orders
→ Highest revenue + highest margin
→ Fewer orders but higher value per order
→ Action: Invest more in Technology marketing
```

### 📈 Insight 5 — Business is Growing (51% in 4 years)

```
2014: $484,247
2015: $470,533 ← Only bad year (2.8% dip)
2016: $609,206 ← Strong recovery
2017: $733,215 ← Best year ever!
Growth: +51.4% from 2014 to 2017
```

### 👥 Insight 6 — Home Office = Hidden Gem

```
Home Office: Smallest segment by revenue ($429K)
BUT: Highest margin at 14.03%!
→ Small but very efficient segment
→ Action: Targeted marketing to Home Office customers
```

### 📦 Insight 7 — 62% Orders are Low Value

```
High   (≥$1000):  468 orders  (4.7%)
Medium (≥$100):  3,300 orders (33.0%)
Low    (<$100):  6,226 orders (62.3%)
→ Most orders are small ticket items
→ AOV improvement strategy needed
```

---

## 10. Interview Q&A — 15 Questions

---

### Q1. What is the difference between a relative and absolute cell reference?

**Answer:**

- **Relative reference** (e.g., `A1`): Changes when the formula is copied to another cell. If `=A1+B1` is in C1 and copied to C2, it becomes `=A2+B2`.
- **Absolute reference** (e.g., `$A$1`): Does not change when copied. The `$` locks the row, column, or both.
- **Mixed reference** (e.g., `$A1` or `A$1`): Locks either the column or row only.

**Example from this project:** When using SUMIF across rows, we used relative references for row numbers (C2, C3...) so AutoFill could automatically adjust for each row.

---

### Q2. When would you use SUMIF over a PivotTable?

**Answer:**

- Use **SUMIF** when you need a fixed, formula-driven answer that updates automatically, is embedded in a structured report, or referenced by other formulas/charts.
- Use **PivotTable** when you need ad-hoc exploration, want to quickly slice data by multiple dimensions, or need to answer questions you haven't pre-defined.

In this project: SUMIF powers the KPI_SUMMARY (fixed structure, feeds dashboard), while PivotTable powers PIVOT_ANALYSIS (flexible exploration).

---

### Q3. What does COUNTA do differently from COUNT?

**Answer:**

- `COUNT` counts only numeric values in a range
- `COUNTA` counts ALL non-empty cells — text, numbers, dates, booleans
- In this project, we used `COUNTA(B2:B9995)` to count orders because Order IDs are text (e.g., "CA-2016-152156"). Using `COUNT` would return 0.

---

### Q4. Why did you use IF() inside the Profit Margin formula?

**Answer:**
The formula `=IF(R2=0, 0, U2/R2)` protects against division by zero. If Sales (R2) equals zero, dividing Profit by Sales would cause a `#DIV/0!` error. The IF catches this edge case and returns 0 instead. This is called **defensive formula writing** — always anticipate edge cases in data.

---

### Q5. Explain the difference between TEXT() and YEAR() functions.

**Answer:**

- `YEAR(date)` → returns a **number** (e.g., 2016). Can be used in calculations, SUMIF criteria, arithmetic.
- `TEXT(date, format)` → returns **text** (e.g., "Nov-16"). Cannot be used in calculations — only for display/labels.

In this project: YEAR() was used for the Year column (needed for SUMIF calculations), TEXT() was used for Month_Year column (needed for chart labels and display only).

---

### Q6. What is a Nested IF and when should you use it?

**Answer:**
A Nested IF places one IF function inside another to handle more than two possible outcomes.

```excel
=IF(R2>=1000,"High", IF(R2>=100,"Medium","Low"))
```

Use when:

- You have 3+ possible outcomes
- Each outcome depends on a different threshold
- Conditions can be ordered from most to least restrictive

**Key rule:** Always write conditions from most restrictive to least restrictive (largest to smallest for numeric thresholds).

---

### Q7. What is the purpose of having a separate RAW_DATA sheet?

**Answer:**
The RAW_DATA sheet serves as the **single source of truth** — the original, unmodified dataset. By keeping it separate:

1. If any formula or transformation goes wrong, the original data is safe
2. You can always trace back to the source
3. It enforces the principle of **non-destructive data processing**
4. Auditors or stakeholders can verify the source data at any time

This is standard practice in professional data analysis environments.

---

### Q8. How does cross-sheet referencing work in Excel?

**Answer:**
Cross-sheet referencing uses the `!` (exclamation mark) operator:

```excel
=SUM(CLEANED_DATA!R:R)
```

Syntax: `SheetName!CellReference`

If the sheet name contains spaces, wrap it in single quotes:

```excel
=SUM('Cleaned Data'!R:R)
```

In this project, the DASHBOARD sheet references KPI_SUMMARY, which references CLEANED_DATA — creating a **data pipeline**: raw data → analysis → visualization.

---

### Q9. What is the difference between a Bar Chart and a Column Chart?

**Answer:**

- **Column Chart**: Vertical bars (bars go up ↑). Best for comparing categories across time or showing rankings.
- **Bar Chart**: Horizontal bars (bars go right →). Best for comparing many categories, especially when labels are long.

In this project: Column chart was used for "Sales by Region" (4 short labels), and Horizontal Bar chart for "Profit by Region" (easier to read region names horizontally).

---

### Q10. What is a Doughnut chart and when is it better than a Pie chart?

**Answer:**
A Doughnut chart is a Pie chart with a hollow center. Benefits over Pie:

- The center can display a total or key metric
- Visually cleaner and more modern
- Easier to compare segment sizes due to arc length vs. area comparison

In this project: Used to show Category split (Furniture 32%, Office Supplies 31%, Technology 37%) — the proportional breakdown is immediately clear.

---

### Q11. What is a PivotTable and what are its four main areas?

**Answer:**
A PivotTable is Excel's built-in tool for dynamically summarizing large datasets without writing formulas. The four areas are:

| Area        | Purpose                        | Example                |
| ----------- | ------------------------------ | ---------------------- |
| **ROWS**    | Categories shown vertically    | Region (East, West...) |
| **COLUMNS** | Categories shown horizontally  | Year (2014, 2015...)   |
| **VALUES**  | What to calculate              | Sum of Sales           |
| **FILTERS** | Global filter for entire table | Ship Mode              |

PivotTables auto-update when source data changes (Refresh required).

---

### Q12. What is data integrity and how did you verify it in this project?

**Answer:**
Data integrity means ensuring data is accurate, consistent, and complete throughout the analysis.

In this project, verification was done by cross-checking the Grand Total across all 5 KPI sections:

```
Section 1 Total Sales → $2,297,200.86 ✅
Section 2 Total Sales → $2,297,200.86 ✅
Section 3 Total Sales → $2,297,200.86 ✅
Section 4 Total Sales → $2,297,200.86 ✅
Section 5 Total Sales → $2,297,200.86 ✅
```

All 5 match — confirming no data was lost or duplicated in any SUMIF formula.

---

### Q13. Why is Profit Margin calculated as Total Profit / Total Sales rather than Average of individual margins?

**Answer:**
Averaging percentages gives mathematically incorrect results when the underlying values have different weights.

**Wrong approach:**

```
Row1: $100 sales, $10 profit = 10%
Row2: $1000 sales, $500 profit = 50%
Average of percentages = (10+50)/2 = 30% ❌
```

**Correct approach:**

```
Total profit: $510
Total sales: $1100
Overall margin: $510/$1100 = 46.4% ✅
```

Always calculate margin as `SUM(Profit)/SUM(Sales)` — never `AVERAGE(Margin%)`.

---

### Q14. What is conditional formatting and how would you use it in this workbook?

**Answer:**
Conditional formatting automatically changes a cell's appearance (color, font, icons) based on its value — without manual formatting.

Use cases in this project:

- **Profit column**: Red fill for negative values (losses), green for positive
- **Margin column**: Color scale — red (low margin) to green (high margin)
- **Sales Band**: Different color per band (High=green, Medium=yellow, Low=red)

Applied through: Home → Conditional Formatting → New Rule → Format cells that contain...

---

### Q15. If a manager asks you to add a new region's data to this dashboard, what steps would you follow?

**Answer:**

1. **Paste new data** into RAW_DATA sheet (below existing rows — do not modify structure)
2. **Copy formulas** in CLEANED_DATA for the new rows (Year, Month_Year, Margin, Band, Days columns)
3. **Update COUNTA range** in KPI_SUMMARY if needed (extend B2:B9995 to new last row)
4. **Refresh PivotTables**: Right-click any PivotTable → Refresh
5. **Dashboard auto-updates**: Since KPI cards and charts reference KPI_SUMMARY, they update automatically once SUMIF formulas recalculate

This demonstrates the **scalability** of the workbook design — the pipeline handles new data gracefully.

---

## Summary — What This Project Demonstrates

| Skill                  | Evidence                                               |
| ---------------------- | ------------------------------------------------------ |
| Data Cleaning          | 5 helper columns, proper formatting                    |
| Formula Writing        | YEAR, TEXT, IF, Nested IF, SUM, SUMIF, COUNTIF, COUNTA |
| Analytical Thinking    | KPI design, cross-section verification                 |
| Data Visualization     | 4 chart types, KPI cards                               |
| Business Communication | Insights framed as business recommendations            |
| Professional Standards | Non-destructive processing, data integrity checks      |
