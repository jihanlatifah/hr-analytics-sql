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

📊 Analysis & Key Findings

1. Attrition Rate by Department

sqlSELECT 
  Department,
  COUNT(*) AS total_employees,
  SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS resigned,
  ROUND(
    100.0 * SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2
  ) AS attrition_rate_pct
FROM employees
GROUP BY Department
ORDER BY attrition_rate_pct DESC;


📸 [Screenshot hasil query — tambahkan setelah dijalankan]



Insight: (Isi setelah analisis selesai — contoh: "Sales department has the highest attrition rate at X%, nearly 2x higher than Research & Development")


2. Overtime vs Attrition

sqlSELECT 
  OverTime,
  COUNT(*) AS total,
  SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) AS resigned,
  ROUND(
    100.0 * SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2
  ) AS resign_rate_pct
FROM employees
GROUP BY OverTime;


📸 [Screenshot hasil query — tambahkan setelah dijalankan]



Insight: (Isi setelah analisis selesai)


3. Employees Earning Above Average Who Still Resigned

sqlSELECT 
  EmployeeNumber, 
  Department, 
  JobRole,
  MonthlyIncome,
  YearsAtCompany
FROM employees
WHERE Attrition = 'Yes'
  AND MonthlyIncome > (SELECT AVG(MonthlyIncome) FROM employees)
ORDER BY MonthlyIncome DESC;


📸 [Screenshot hasil query — tambahkan setelah dijalankan]



Insight: (Isi setelah analisis selesai — menunjukkan salary bukan satu-satunya faktor retensi)


4. Top 3 Highest-Paid Employees per Department

sqlWITH salary_ranked AS (
  SELECT 
    EmployeeNumber,
    Department,
    JobRole,
    MonthlyIncome,
    RANK() OVER (
      PARTITION BY Department 
      ORDER BY MonthlyIncome DESC
    ) AS salary_rank
  FROM employees
)
SELECT * FROM salary_ranked
WHERE salary_rank <= 3;


📸 [Screenshot hasil query — tambahkan setelah dijalankan]




5. Department Summary: Salary, Tenure & Performance

sqlSELECT 
  Department,
  COUNT(*) AS total_employees,
  ROUND(AVG(MonthlyIncome), 0) AS avg_salary,
  ROUND(AVG(YearsAtCompany), 1) AS avg_tenure_years,
  ROUND(AVG(PerformanceRating), 2) AS avg_performance_rating,
  ROUND(
    100.0 * SUM(CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2
  ) AS attrition_rate_pct
FROM employees
GROUP BY Department
ORDER BY avg_salary DESC;


📸 [Screenshot hasil query — tambahkan setelah dijalankan]



Insight: (Isi setelah analisis selesai)


💡 Key Insights Summary




Highest attrition department: ...
Overtime impact: Employees with overtime are X% more likely to resign
Salary is not everything: X employees above average salary still resigned
Tenure pattern: Department X has the longest average tenure at X years
Top performer distribution: ...
