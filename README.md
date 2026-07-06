# 👥 HR Analytics: Employee Attrition & Performance Analysis

## 📌 Project Overview

Employee attrition (turnover) is one of the most costly challenges for any organization. This project uses SQL to analyze patterns in employee resignation, salary distribution, overtime behavior, and performance ratings — helping HR teams make more data-driven workforce decisions.

Dataset: **IBM HR Analytics Employee Attrition & Performance** (Kaggle)
Records: **1,470 employees** | **35 attributes**

---

## ❓ Business Questions

| # | Question | SQL Technique |
|---|---|---|
| 1 | Which department has the highest attrition rate? | GROUP BY, CASE WHEN |
| 2 | Does salary correlate with employee resignation? | Subquery, AVG |
| 3 | Do employees with overtime tend to resign more? | GROUP BY, CASE WHEN |
| 4 | What is the average tenure per department? | AVG, GROUP BY |
| 5 | Who are the top performers in each department? | Window Function, RANK() |
| 6 | What is the salary distribution by job level? | CTE, GROUP BY |
| 7 | Which factors most distinguish employees who stay vs resign? | Multi-condition WHERE, JOIN |

---
## 📁 Project Structure

```
hr-analytics-sql/
│
├── README.md
├── queries/
│   ├── 01_basic_exploration.sql       # Data overview & sanity checks
│   ├── 02_attrition_analysis.sql      # Attrition by dept, overtime, salary
│   ├── 03_salary_performance.sql      # Salary distribution & top performers
│   └── 04_advanced_cte_window.sql     # CTE & window functions
└── results/
    └── screenshots/                   # Query result screenshots
```

---

## 📂 Dataset

| Detail | Info |
|---|---|
| Source | [IBM HR Analytics — Kaggle](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset) |
| Records | 1,470 employees |
| Key Columns | Attrition, Department, MonthlyIncome, OverTime, YearsAtCompany, PerformanceRating, JobLevel |
| License | Public / Open |

---

## 🛠️ Tools

- **SQLite** / **PostgreSQL** — query execution
- **DB Browser for SQLite** / **DBeaver** — GUI interface
- **Python (pandas)** — initial data import & validation

---
