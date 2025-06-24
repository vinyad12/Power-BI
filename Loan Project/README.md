
# 📊 Financial Risk Analysis Dashboard (Power BI)

This project focuses on the visual analysis of financial loan data, aiming to uncover insights related to **loan distribution**, **default risk**, **demographic factors**, and **financial behavior patterns**. The dashboard provides a comprehensive view of various KPIs to support risk mitigation and strategic lending.

---

## 📁 Table of Contents

- [Overview](#overview)
- [Dashboard Tabs](#dashboard-tabs)
- [Key Findings](#key-findings)
- [DAX Measures Used](#dax-measures-used)
- [Technologies](#technologies)
- [Screenshots](#screenshots)

---

## 📌 Overview

This Power BI dashboard analyzes historical loan data to track:
- Year-over-Year changes in loan issuance and default
- Loan behavior across demographics (age, income, employment, marital status)
- Risk segmentation using credit scores and DTI ratios
- Default trends over time and employment groups

---

## 📊 Dashboard Tabs

### 1. **Loan Default Overview**
- **Loan Amount By Purpose**: Highest borrowing for Home, followed by Business.
- **Average Loan By Age Group**: Adults had the highest average loan, teens the lowest.
- **Default Rate By Employment Type**: Unemployed group has the highest default rate.
- **Default By (%) Year**: Slight volatility from 2013 to 2018.

### 2. **Applicant Demographics And Financial Profile**
- **Median Loan Amount by Credit Score**: Borrowers with low scores had the highest median loan.
- **Average Loan by Marital Status & Age Group (High Credit)**: Senior Citizens and Adults are more consistent in high loan averages.
- **Total Loan by Education**: Higher loan amounts are associated with lower education levels.
- **Middle-Aged Loan Distribution**: Mortgage and dependent status have minimal influence on total loan.

### 3. **Financial Risk Metrics**
- **YOY Loan Amount Change**: Fluctuations with highs in 2015 (+1.80) and 2018 (+1.73).
- **YOY Default Loan Change**: Peak default in 2015 (+2.7), major drop in 2017 (-2.8).
- **YTD Loan Amount by Credit Score & Marital Status**: Medium and high credit scores dominate in volume.
- **Loan Amount by Income Bracket and Employment Type**: High income with full-time employment shows the highest borrowing pattern.

---

## 📌 Key Findings

- **Employment Type**: Strong correlation between employment status and default risk.
- **Credit Score**: Lower scores are not always linked to lower loans, contrary to expectations.
- **Income & Education**: Borrowers with lower education levels surprisingly receive higher loans.
- **YOY Trends**: Loan amounts and defaults show inconsistent trends; macroeconomic factors could play a role.
- **Demographics**: Adults and Middle Adults dominate the loan segment, regardless of dependent status.

---

## 🧮 DAX Measures Used

```dax
-- YOY Loan Amount Change
YOY Loan Amount Change = 
VAR PrevYear = CALCULATE(SUM(Loan_default[LoanAmount]), DATEADD(Loan_default[Date], -1, YEAR))
VAR CurrentYear = SUM(Loan_default[LoanAmount])
RETURN DIVIDE(CurrentYear - PrevYear, PrevYear)

-- YOY Default Loan Change
YOY Default Loan Change = 
VAR PrevYearDefault = CALCULATE(SUM(Loan_default[Default]), DATEADD(Loan_default[Date], -1, YEAR))
VAR CurrentYearDefault = SUM(Loan_default[Default])
RETURN DIVIDE(CurrentYearDefault - PrevYearDefault, PrevYearDefault)

-- Default Rate By Employment Type
Default Rate = 
DIVIDE(SUM(Loan_default[Default]), COUNT(Loan_default[Default]))

-- Median By Credit Score Bins
Median Loan = 
MEDIANX(
    VALUES(Loan_default[Credit Score Bins]),
    CALCULATE(SUM(Loan_default[LoanAmount]))
)

-- Average Loan Amount (High Credit)
Average Loan Amount (High Credit) = 
CALCULATE(
    AVERAGE(Loan_default[LoanAmount]),
    Loan_default[CreditScore] >= 700
)

-- Total Loan by Education Type
Total Loan by Education = 
SUM(Loan_default[LoanAmount])
```

> _Note_: DAX measures were applied using calculated columns and visuals were segmented with filters and slicers for `Age Group`, `Employment Type`, `Income Bracket`, and `Marital Status`.

---

## 🛠 Technologies

- **Power BI Desktop**
- **DAX (Data Analysis Expressions)**
- **Data Modelling**
- **Slicers, Filters & Bookmarks**
- **Custom Visuals (Sankey, Donut, Area Graphs)**

---



## 📬 Contact

If you have any suggestions or questions, feel free to reach out via www.linkedin.com/in/vinay-yadav98 or open an issue on this repository.
