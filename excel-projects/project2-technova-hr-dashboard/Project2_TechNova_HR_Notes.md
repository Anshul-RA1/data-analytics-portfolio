# Project 2 — TechNova HR Workforce Analytics Dashboard

### Excel Data Analytics Portfolio | Anshul Raghuvanshi

---

## 📋 Table of Contents

1. [Project Overview](#1-project-overview)
2. [Business Case & User Story](#2-business-case--user-story)
3. [Dataset Details](#3-dataset-details)
4. [Workbook Structure](#4-workbook-structure)
5. [Formulas Explained](#5-formulas-explained)
6. [Key Concepts Discussed](#6-key-concepts-discussed)
7. [KPI Summary Analysis](#7-kpi-summary-analysis)
8. [PivotTable Analysis](#8-pivottable-analysis)
9. [Dashboard Design](#9-dashboard-design)
10. [Key Business Insights](#10-key-business-insights)
11. [Interview Q&A — 15 Questions](#11-interview-qa--15-questions)

---

## 1. Project Overview

| Field                  | Details                                                                      |
| ---------------------- | ---------------------------------------------------------------------------- |
| **Project Name**       | TechNova HR Workforce Analytics Dashboard                                    |
| **Tool Used**          | Microsoft Excel 365                                                          |
| **Dataset**            | IBM HR Analytics Employee Attrition                                          |
| **Level**              | Moderate — Project 2 of 3                                                    |
| **Employees Analyzed** | 1,470                                                                        |
| **Columns**            | 35 original + 6 helper = 41 total                                            |
| **Sheets Built**       | 6 (RAW_DATA, CLEANED_DATA, KPI_SUMMARY, PIVOT_ANALYSIS, DASHBOARD, INSIGHTS) |

### What Was Built

A complete HR analytics workbook analyzing employee attrition patterns across departments, age groups, salary bands, and gender — with an interactive dashboard, insights sheet, and live KPI metrics.

---

## 2. Business Case & User Story

### Business Context

**TechNova Solutions** (fictional) — an IT company with 1,470 employees across 3 departments (HR, R&D, Sales) and 9 job roles. The CHRO is concerned about rising attrition, potential gender pay gaps, and tenure distribution.

### The Problem

```
❓ Overall attrition rate = 16.12% — above 10-15% benchmark
❓ Which department is most at risk?
❓ Does salary directly impact attrition?
❓ Are young employees leaving faster?
❓ Is there a gender pay gap?
```

### User Story

> _"As the CHRO, I need to slice HR data by department, gender, age group and job role to understand attrition patterns — so I can design targeted retention programs and present findings to the Board quarterly."_

### Solution Delivered

A 6-sheet Excel workbook with:

- 6 helper columns using advanced formulas
- 5-section KPI analysis (COUNTIFS, AVERAGEIFS, MAXIFS, MINIFS)
- 3 PivotTables for multi-dimensional analysis
- Interactive dashboard with 6 KPI cards + 4 charts
- Dedicated INSIGHTS sheet with executive summary + recommendations

---

## 3. Dataset Details

| Field             | Value                                                                            |
| ----------------- | -------------------------------------------------------------------------------- |
| **Source**        | Kaggle — IBM HR Analytics                                                        |
| **URL**           | https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset |
| **File**          | WA*Fn-UseC*-HR-Employee-Attrition.csv                                            |
| **Rows**          | 1,470 employees                                                                  |
| **Columns**       | 35                                                                               |
| **Null Values**   | 0 — perfectly clean!                                                             |
| **Target Column** | Attrition (Yes=237, No=1233)                                                     |

### Key Columns Used

| Column          | Letter | Description             |
| --------------- | ------ | ----------------------- |
| Age             | A      | Employee age (18-60)    |
| Attrition       | B      | Yes/No — left company?  |
| Department      | E      | HR / R&D / Sales        |
| Gender          | L      | Male / Female           |
| JobRole         | P      | 9 different roles       |
| JobSatisfaction | Q      | 1-4 rating              |
| MonthlyIncome   | S      | Salary ($1,009-$19,999) |
| OverTime        | W      | Yes/No                  |
| YearsAtCompany  | AF     | Tenure (0-40 years)     |

---

## 4. Workbook Structure

```
Project2_TechNova_HR_Dashboard.xlsx
│
├── 📋 RAW_DATA          (Gray tab)   — 1,470 rows × 35 cols — untouched
├── 🧹 CLEANED_DATA      (Blue tab)   — 1,470 rows × 41 cols — 6 helper cols
├── 📊 KPI_SUMMARY       (Red tab)    — 6 sections, all formulas
├── 🔄 PIVOT_ANALYSIS    (Green tab)  — 3 PivotTables
├── 🎨 DASHBOARD         (Gold tab)   — 6 KPI cards + 4 charts
└── 💡 INSIGHTS          (Purple tab) — Executive insights + recommendations
```

---

## 5. Formulas Explained

### 5.1 IF() — Attrition_Num Helper Column

**Column AJ — Converts Yes/No text to 1/0 numbers**

```excel
=IF(B2="Yes", 1, 0)
```

**Why needed:**

```
"Yes"/"No" text → Cannot SUM or calculate rates
1/0 numbers    → Can SUM, AVERAGE, calculate %

Attrition Rate = SUM(Attrition_Num) / COUNT(Employees)
               = 237 / 1470 = 16.12%
```

**Result:** Yes=1, No=0 across all 1,470 rows

---

### 5.2 Nested IF() — Age_Band Helper Column

**Column AK — Categorizes employees by age group**

```excel
=IF(A2<=25,"Young", IF(A2<=35,"Mid", IF(A2<=45,"Experienced","Veteran")))
```

**Logic flow:**

```
Age 41:
Step 1: 41 <= 25? NO → continue
Step 2: 41 <= 35? NO → continue
Step 3: 41 <= 45? YES → "Experienced" ✅
```

**Results:**

- Young (18-25): 123 employees
- Mid (26-35): 606 employees
- Experienced (36-45): 468 employees
- Veteran (46+): 273 employees

---

### 5.3 Nested IF() — Salary_Band Helper Column

**Column AL — Categorizes by salary level**

```excel
=IF(S2<3000,"Low", IF(S2<7000,"Mid", IF(S2<12000,"High","Premium")))
```

**Bands:**

- Low (<$3,000): 395 employees
- Mid ($3,000-$7,000): 640 employees
- High ($7,000-$12,000): 240 employees
- Premium (≥$12,000): 195 employees

---

### 5.4 Nested IF() — Experience_Level Helper Column

**Column AM — Categorizes by years at company**

```excel
=IF(AF2<=2,"Junior", IF(AF2<=5,"Mid", IF(AF2<=10,"Senior","Veteran")))
```

---

### 5.5 CHOOSE() — Satisfaction_Label Helper Column ← NEW!

**Column AN — Converts numeric rating to label**

```excel
=CHOOSE(Q2, "Low", "Medium", "High", "Very High")
```

**How CHOOSE works:**

```
CHOOSE(index_number, value1, value2, value3, value4)
       │               │       │       │       │
       Q2=1            Low     Medium  High    Very High

Q2=1 → "Low"
Q2=2 → "Medium"
Q2=3 → "High"
Q2=4 → "Very High"
```

**CHOOSE vs Nested IF:**

```
Nested IF:  =IF(Q2=1,"Low",IF(Q2=2,"Medium",IF(Q2=3,"High","Very High")))
CHOOSE:     =CHOOSE(Q2,"Low","Medium","High","Very High")

CHOOSE is cleaner when values are sequential numbers (1,2,3,4...)
Nested IF works for any condition type
```

---

### 5.6 AVERAGEIF() — Income_vs_Avg Helper Column ← NEW!

**Column AO — Compares each employee's salary to department average**

```excel
=IF(S2>=AVERAGEIF($E$2:$E$1471, E2, $S$2:$S$1471), "Above Avg", "Below Avg")
```

**Breaking it down:**

```
AVERAGEIF($E$2:$E$1471, E2, $S$2:$S$1471)
          │               │    │
          Department col  This  Salary col
          (ABSOLUTE)      row's (ABSOLUTE)
                          dept
                          (RELATIVE)

→ Calculates average salary for THIS employee's department ONLY
→ Compares individual salary to their department's average
```

**Why $ (Absolute Reference)?**

```
$E$2:$E$1471 → Range never changes when formula copies down
E2           → Changes each row (E2→E3→E4...) — RELATIVE
$S$2:$S$1471 → Range never changes — ABSOLUTE

Rule: Ranges that span full data = ABSOLUTE ($)
      Current row reference = RELATIVE (no $)
```

**Result:**

- Above Avg: 483 employees (33%)
- Below Avg: 987 employees (67%)

---

### 5.7 COUNTIFS() — Multiple Condition Count ← NEW!

**Used in KPI_SUMMARY Sections 2, 3, 5**

```excel
=COUNTIFS(range1, criteria1, range2, criteria2)
```

**Example — Sales employees who left:**

```excel
=COUNTIFS(CLEANED_DATA!E2:E1471, "Sales",
          CLEANED_DATA!B2:B1471, "Yes")
→ 92
```

**COUNTIF vs COUNTIFS:**

```
COUNTIF  → ONE condition
           =COUNTIF(E:E, "Sales") → 446 (all Sales employees)

COUNTIFS → MULTIPLE conditions
           =COUNTIFS(E:E,"Sales", B:B,"Yes") → 92 (Sales who LEFT)
```

---

### 5.8 AVERAGEIFS() — Multiple Condition Average ← NEW!

**Used in KPI_SUMMARY Section 4**

```excel
=AVERAGEIFS(avg_range, range1, criteria1, range2, criteria2)
```

**Critical difference from AVERAGEIF:**

```
AVERAGEIF  → avg_range is LAST
             =AVERAGEIF(dept_col, "Sales", salary_col)

AVERAGEIFS → avg_range is FIRST
             =AVERAGEIFS(salary_col, dept_col, "Sales", gender_col, "Female")
```

**Example — Sales Female average salary:**

```excel
=AVERAGEIFS(CLEANED_DATA!S2:S1471,
            CLEANED_DATA!E2:E1471, "Sales",
            CLEANED_DATA!L2:L1471, "Female")
→ $6,972
```

---

### 5.9 MAXIFS() — Conditional Maximum ← NEW!

**Used in KPI_SUMMARY Section 4**

```excel
=MAXIFS(max_range, criteria_range, criteria)
```

**Example — Highest salary in R&D:**

```excel
=MAXIFS(CLEANED_DATA!S2:S1471,
        CLEANED_DATA!E2:E1471, "Research & Development")
→ $19,999
```

**MAX vs MAXIFS:**

```
MAX   → Entire dataset maximum (no filter)
        =MAX(S:S) → $19,999 (could be any dept)

MAXIFS → Department-specific maximum
         =MAXIFS(S:S, E:E, "Sales") → $19,847 (Sales only)
```

---

### 5.10 MINIFS() — Conditional Minimum ← NEW!

```excel
=MINIFS(min_range, criteria_range, criteria)
```

**Example — Lowest salary in HR:**

```excel
=MINIFS(CLEANED_DATA!S2:S1471,
        CLEANED_DATA!E2:E1471, "Human Resources")
→ $1,555
```

**Formula Family Summary:**

```
Function    No Condition    One Condition    Multiple
SUM         SUM()           SUMIF()          SUMIFS()
COUNT       COUNT()         COUNTIF()        COUNTIFS()
AVERAGE     AVERAGE()       AVERAGEIF()      AVERAGEIFS()
MAX         MAX()           MAXIFS()         MAXIFS()
MIN         MIN()           MINIFS()         MINIFS()
```

---

## 6. Key Concepts Discussed

### 6.1 AVERAGE vs AVERAGEIF — Why Total Row Uses AVERAGE

**Question:** Why use `=AVERAGE(S:S)` in total row instead of averaging department averages?

**Answer — Weighted Average Problem:**

```
Wrong approach (averaging dept averages):
HR    avg: $6,655  (63 employees)
R&D   avg: $6,281  (961 employees)
Sales avg: $6,959  (446 employees)
Simple avg: ($6,655+$6,281+$6,959)/3 = $6,632 ❌ WRONG!

Correct approach:
=AVERAGE(all 1470 salary values) = $6,503 ✅

Why different?
R&D has 961 employees — should have much more weight!
Simple average of dept averages treats all depts equally.
AVERAGE of raw data automatically weights by size.
```

**Rule:** Never average the averages — always go back to raw data!

---

### 6.2 Absolute vs Relative Reference

```
Relative  → Changes when formula copies: E2→E3→E4
Absolute  → Never changes: $E$2:$E$1471

In AVERAGEIF:
=AVERAGEIF($E$2:$E$1471, E2, $S$2:$S$1471)
            ↑ ABSOLUTE       ↑ RELATIVE   ↑ ABSOLUTE
            Full range       Current row  Full range
            never changes    changes      never changes
```

---

### 6.3 Conditional Formatting — 3 Types Used

```
Type 1 — Cell Rules (Attrition Rate):
> 18% → Red fill + White font (Critical!)
< 15% → Green fill + White font (Good!)
Between → Orange fill (Warning)

Type 2 — Color Scale (Salary columns):
Green (high) → Yellow → Red (low)
Automatically detects min/max!

Type 3 — Data Bars (Staff counts):
In-cell bar chart — visual proportion instantly visible!
```

---

### 6.4 Custom Number Format

```
Format Code     Value     Display
0.0" yrs"       7.008     7.0 yrs
$#,##0,"K"      6500      $7K
0.00"%"         0.1612    16.12%
"Age: "0.0      36.9      Age: 36.9
```

---

## 7. KPI Summary Analysis

### Section 1 — Overall HR KPIs

| KPI                | Value   | Formula                        |
| ------------------ | ------- | ------------------------------ |
| Total Employees    | 1,470   | `=COUNTA(A2:A1471)`            |
| Employees Left     | 237     | `=SUM(AJ2:AJ1471)`             |
| Attrition Rate     | 16.12%  | `=SUM(AJ:AJ)/COUNTA(A2:A1471)` |
| Avg Monthly Salary | $6,503  | `=AVERAGE(S2:S1471)`           |
| Avg Age            | 36.9    | `=AVERAGE(A2:A1471)`           |
| Avg Tenure         | 7.0 yrs | `=AVERAGE(AF2:AF1471)`         |
| Overtime Employees | 416     | `=COUNTIF(W:W,"Yes")`          |
| Active Employees   | 1,233   | `=COUNTA(A:A)-SUM(AJ:AJ)`      |

### Section 2 — Attrition by Department

| Department             | Total     | Left    | Active    | Rate       | Avg Salary |
| ---------------------- | --------- | ------- | --------- | ---------- | ---------- |
| Human Resources        | 63        | 12      | 51        | 19.05% 🔴  | $6,655     |
| Research & Development | 961       | 133     | 828       | 13.84% 🟢  | $6,281     |
| Sales                  | 446       | 92      | 354       | 20.63% 🔴  | $6,959     |
| **Total**              | **1,470** | **237** | **1,233** | **16.12%** | **$6,503** |

### Section 3 — Attrition by Gender

| Gender    | Total     | Left    | Active    | Rate       | Avg Salary |
| --------- | --------- | ------- | --------- | ---------- | ---------- |
| Female    | 588       | 87      | 501       | 14.80% 🟢  | $6,687     |
| Male      | 882       | 150     | 732       | 17.01% 🟠  | $6,381     |
| **Total** | **1,470** | **237** | **1,233** | **16.12%** | **$6,503** |

### Section 4 — Salary Analysis by Department

| Department | Avg All    | Avg Male   | Avg Female | Max         | Min        |
| ---------- | ---------- | ---------- | ---------- | ----------- | ---------- |
| HR         | $6,655     | $6,371     | $7,264     | $19,717     | $1,555     |
| R&D        | $6,281     | $6,130     | $6,514     | $19,999     | $1,009     |
| Sales      | $6,959     | $6,950     | $6,972     | $19,847     | $1,052     |
| **Total**  | **$6,503** | **$6,381** | **$6,687** | **$19,999** | **$1,009** |

### Section 5 — Attrition by Age Band

| Age Band            | Total     | Left    | Active    | Rate       | Avg Salary |
| ------------------- | --------- | ------- | --------- | ---------- | ---------- |
| Young (18-25)       | 123       | 44      | 79        | 35.77% 🔴  | $2,973     |
| Mid (26-35)         | 606       | 116     | 490       | 19.14% 🔴  | $4,896     |
| Experienced (36-45) | 468       | 43      | 425       | 9.19% 🟢   | $7,104     |
| Veteran (46+)       | 273       | 34      | 239       | 12.45% 🟢  | $10,630    |
| **Total**           | **1,470** | **237** | **1,233** | **16.12%** | **$6,503** |

### Section 6 — Attrition by Salary Band

| Salary Band     | Total | Left | Rate      |
| --------------- | ----- | ---- | --------- |
| Low (<$3K)      | 395   | 113  | 28.61% 🔴 |
| Mid ($3K-$7K)   | 640   | 77   | 12.03% 🟢 |
| High ($7K-$12K) | 240   | 36   | 15.00% 🟠 |
| Premium (≥$12K) | 195   | 11   | 5.64% 🟢  |

---

## 8. PivotTable Analysis

### PivotTable 1 — Department × Attrition

| Department | No        | Yes     | Total     |
| ---------- | --------- | ------- | --------- |
| HR         | 51        | 12      | 63        |
| R&D        | 828       | 133     | 961       |
| Sales      | 354       | 92      | 446       |
| **Total**  | **1,233** | **237** | **1,470** |

### PivotTable 2 — Age Band × Job Role

All 9 job roles × 4 age bands → 36-cell matrix
Key finding: No young employees in Manager role!

### PivotTable 3 — Salary Band × Attrition

```
Low:     282 No | 113 Yes → 28.61% attrition
Mid:     563 No |  77 Yes → 12.03% attrition
High:    204 No |  36 Yes → 15.00% attrition
Premium: 184 No |  11 Yes →  5.64% attrition
```

---

## 9. Dashboard Design

### KPI Cards

| Card            | Formula           | Color  |
| --------------- | ----------------- | ------ |
| Total Employees | `=KPI_SUMMARY!D4` | Blue   |
| Attrition Count | `=KPI_SUMMARY!D5` | Red    |
| Attrition Rate  | `=KPI_SUMMARY!D6` | Orange |
| Avg Salary      | `=KPI_SUMMARY!D7` | Green  |
| Avg Age         | `=KPI_SUMMARY!D8` | Purple |
| Avg Tenure      | `=KPI_SUMMARY!D9` | Teal   |

### Charts

| Chart                    | Type           | Key Insight               |
| ------------------------ | -------------- | ------------------------- |
| Attrition by Department  | Column         | Sales worst (20.63%)      |
| Avg Salary by Department | Horizontal Bar | Sales highest ($6,959)    |
| Attrition by Age Band    | Column         | Young worst (35.77%)      |
| Attrition by Salary Band | Column         | Low salary worst (28.61%) |

---

## 10. Key Business Insights

### 🔴 Critical Findings

```
1. Sales Attrition = 20.63%
   → Highest department — immediate action needed
   → Despite highest avg salary ($6,959)!
   → Money alone not keeping Sales employees

2. Young Employees (18-25) = 35.77% attrition
   → Over 1 in 3 young employees leaves!
   → Lowest avg salary ($2,973) — direct correlation
   → Need mentorship + career growth programs

3. Low Salary Band = 28.61% attrition
   → 5x higher than Premium band (5.64%)
   → Cost of rehiring >> Cost of salary raise
   → 395 employees at risk

4. Overtime Employees = 30.5% vs 10.4% (no OT)
   → Overtime = 3x higher attrition!
   → Sales has most overtime → explains their high rate
```

### 🟠 Warning Signals

```
1. HR Dept = 19.05% — above benchmark
2. Male attrition 17.01% vs Female 14.80%
3. Mid age band 19.14% — second highest
4. High salary still 15% — non-monetary issues
```

### 🟢 Positive Findings

```
1. R&D = 13.84% — best department
2. Premium salary = only 5.64% attrition
3. Veteran employees = 6.96% — very stable
4. Female attrition 14.80% — below benchmark
5. Females earn MORE than males in all 3 depts!
   → No gender pay gap issue — reverse gap!
```

### 💡 Strategic Recommendations

| Priority  | Action                  | Expected Impact         |
| --------- | ----------------------- | ----------------------- |
| 🔴 HIGH   | Raise Low band salaries | 28%→12% attrition       |
| 🔴 HIGH   | Reduce Sales overtime   | 30.5%→10% attrition     |
| 🔴 HIGH   | Young employee program  | Retain 18-25 group      |
| 🟠 MEDIUM | Replicate R&D culture   | Improve Sales retention |
| 🟢 LOW    | Male retention review   | Close gender gap        |

---

## 11. Interview Q&A — 15 Questions

---

### Q1. What is the difference between COUNTIF and COUNTIFS?

**Answer:**

- `COUNTIF` counts cells matching **one** condition
- `COUNTIFS` counts cells matching **multiple** conditions simultaneously

```excel
COUNTIF  → =COUNTIF(E:E, "Sales")
            → 446 (all Sales employees)

COUNTIFS → =COUNTIFS(E:E, "Sales", B:B, "Yes")
            → 92 (Sales employees who LEFT)
```

Key syntax difference: COUNTIFS accepts pairs of range+criteria, unlimited.

---

### Q2. What is the difference between AVERAGEIF and AVERAGEIFS?

**Answer:**

- `AVERAGEIF(range, criteria, avg_range)` — ONE condition, avg_range is **last**
- `AVERAGEIFS(avg_range, range1, criteria1, range2, criteria2)` — MULTIPLE conditions, avg_range is **first**

```excel
AVERAGEIF  → avg_range LAST
AVERAGEIFS → avg_range FIRST ← Most common mistake!
```

---

### Q3. Why did you use AVERAGE() in the total row instead of averaging the department averages?

**Answer:**
Averaging department averages creates a weighted average problem. Since R&D has 961 employees and HR has only 63, treating them equally distorts the result. `=AVERAGE(raw_salary_column)` automatically weights each employee equally, giving the mathematically correct overall average ($6,503 vs incorrect $6,632).

---

### Q4. What is the CHOOSE() function and when is it better than nested IF?

**Answer:**
`CHOOSE(index, value1, value2, value3...)` selects from a list based on a number.

```excel
=CHOOSE(Q2,"Low","Medium","High","Very High")
```

Better than nested IF when:

- Input is sequential numbers (1,2,3,4)
- More readable and shorter code
- Easier to maintain

Nested IF is better when conditions are complex or non-sequential.

---

### Q5. What is an absolute reference and why is it critical in AVERAGEIF?

**Answer:**
Absolute reference (`$E$2:$E$1471`) locks a cell range so it doesn't shift when the formula is copied down.

In AVERAGEIF, the lookup range and average range must stay fixed (absolute) while only the criteria cell changes per row (relative):

```excel
=AVERAGEIF($E$2:$E$1471, E2, $S$2:$S$1471)
            ↑ ABSOLUTE   ↑RELATIVE ↑ABSOLUTE
```

Without `$`, copying the formula down would shift the ranges, giving wrong results.

---

### Q6. What is MAXIFS and how does it differ from MAX?

**Answer:**

- `MAX(range)` → highest value in entire range, no filter
- `MAXIFS(max_range, criteria_range, criteria)` → highest value for matching rows only

```excel
MAX(S:S)                          → $19,999 (any department)
MAXIFS(S:S, E:E, "Sales")        → $19,847 (Sales only)
MAXIFS(S:S, E:E, "R&D")          → $19,999 (R&D only)
```

---

### Q7. What is conditional formatting and what are its 3 main types?

**Answer:**
Conditional formatting automatically changes cell appearance based on value — without manual formatting.

3 types used in this project:

1. **Cell Rules** — Attrition >18% = Red, <15% = Green
2. **Color Scales** — Salary columns: green (high) to red (low)
3. **Data Bars** — In-cell bar charts showing proportion

---

### Q8. Why is attrition rate calculated as SUM/COUNTA instead of using the Attrition column directly?

**Answer:**
The Attrition column contains "Yes"/"No" text — you cannot perform math on text. By creating the `Attrition_Num` helper column (Yes=1, No=0), we convert text to numbers enabling:

```
=SUM(AJ:AJ)           → Count of leavers (237)
=SUM(AJ:AJ)/COUNTA(A:A) → Attrition rate (16.12%)
```

---

### Q9. What business insight surprised you most in this dataset?

**Answer:**
The salary paradox in Sales: Sales has the **highest average salary** ($6,959) yet the **highest attrition** (20.63%). This proves that salary alone doesn't retain employees — factors like work culture, overtime burden, and career growth matter equally. R&D has the **lowest salary** ($6,281) yet the **lowest attrition** (13.84%).

---

### Q10. How does CHOOSE() differ from a lookup table?

**Answer:**

- `CHOOSE()` is best for small sequential numeric lists (1-254 values)
- VLOOKUP/XLOOKUP is better for larger, non-sequential mappings stored in a table

For 4-level satisfaction ratings (1=Low, 2=Medium, 3=High, 4=Very High), CHOOSE() is simpler and faster than creating a lookup table.

---

### Q11. What is the Weighted Average problem and how did you handle it?

**Answer:**
Simple averaging of group averages gives wrong results when groups have different sizes. Example:

```
HR (63 employees) avg: $6,655
R&D (961 employees) avg: $6,281
Simple avg: ($6,655+$6,281)/2 = $6,468 ❌

Correct: =AVERAGE(all 1470 values) = $6,503 ✅
R&D's 961 employees properly outweigh HR's 63.
```

---

### Q12. How would you add a new department's data to this dashboard?

**Answer:**

1. Paste new rows in RAW_DATA (below existing data)
2. Extend CLEANED_DATA formulas for new rows (double-click fill handle)
3. Add new department row in KPI_SUMMARY with same COUNTIFS formulas
4. Refresh all 3 PivotTables (right-click → Refresh)
5. Dashboard auto-updates via KPI_SUMMARY links

---

### Q13. What is the INSIGHTS sheet and why is it important?

**Answer:**
The INSIGHTS sheet translates raw numbers into business language — Executive Summary, Critical Findings, Warning Signals, Positive Findings, and Strategic Recommendations. It uses live formulas linking to KPI_SUMMARY so it auto-updates. This is the sheet a CEO or CHRO would read — they don't look at raw data or formulas.

---

### Q14. Why did you use a horizontal bar chart for salary and column chart for attrition?

**Answer:**

- **Horizontal Bar** (Salary): Department names are long text — horizontal layout gives more space for labels, easier to read
- **Column Chart** (Attrition): Comparison between categories where order matters (Low→Premium showing clear trend) — vertical bars make the trend direction clearer

Chart type selection should always match the story you're telling.

---

### Q15. If attrition in Sales improved to 12% next month, how would that reflect in your workbook?

**Answer:**

1. New data added to RAW_DATA with updated Attrition values
2. CLEANED_DATA helper columns auto-recalculate via formulas
3. KPI_SUMMARY COUNTIFS/AVERAGEIFS formulas auto-recalculate
4. Dashboard KPI cards auto-update (linked to KPI_SUMMARY)
5. PivotTables need one manual Refresh (right-click → Refresh)
6. INSIGHTS sheet Live KPI section auto-updates

This demonstrates the **scalable pipeline design** — minimum manual work when data changes.

---

## Summary — Skills Demonstrated

| Skill                  | Evidence                                           |
| ---------------------- | -------------------------------------------------- |
| Advanced Formulas      | COUNTIFS, AVERAGEIFS, MAXIFS, MINIFS, CHOOSE       |
| Data Transformation    | 6 helper columns, conditional categorization       |
| Statistical Analysis   | Weighted avg, attrition rate, salary distribution  |
| Conditional Formatting | 3 types: Cell Rules, Color Scale, Data Bars        |
| Visualization          | 4 charts, 6 KPI cards, color-coded insights        |
| Business Communication | INSIGHTS sheet with exec summary + recommendations |
| Data Integrity         | All totals cross-verified: 1,470 ✓ 237 ✓ 16.12% ✓  |
| Custom Formatting      | "7.0 yrs", "$6K", percentage formats               |
