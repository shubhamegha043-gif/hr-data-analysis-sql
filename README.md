# 📊 HR Data Analysis (SQL)
SQL-based analysis of HR dataset to extract employee insights and trends


## 📌 Project Overview

This project analyzes HR dataset using SQL to extract insights about employee attrition, department performance, and job satisfaction. Advanced SQL techniques like aggregations and crosstab functions are used to uncover meaningful patterns.

---

## 📂 Dataset Information

The dataset contains employee-related information such as:

* Department
* Attrition (Yes/No)
* Gender
* Job Role
* Job Satisfaction
* Employee Count

---

## 🎯 Objectives

* Analyze attrition across departments
* Identify gender-based attrition trends
* Explore job satisfaction distribution
* Understand workforce patterns

---

## 🛠 Tools Used

* PostgreSQL
* SQL (pgAdmin)

---

## 📊 Analysis Performed

### 🔹 Department-wise Attrition

* Counted number of employees leaving in each department
* Calculated attrition contribution per department

### 🔹 Gender-based Attrition

* Focused on female employee attrition
* Calculated percentage contribution by department

### 🔹 Job Satisfaction Analysis (Crosstab)

* Used `crosstab()` function (tablefunc extension)
* Transformed rows into columns for better analysis
* Compared satisfaction levels across job roles

---

## 📈 Key Insights

### ✅ Department Attrition

* **R&D** has the highest attrition
* Followed by **Sales**, then **HR**

### ✅ Female Attrition Analysis

* R&D contributes ~49% of female attrition
* Sales contributes ~43%
* Indicates higher attrition concentration in these departments

### ✅ Job Satisfaction Trends

* Crosstab shows distribution of satisfaction levels (1–4) across roles
* Roles like **Laboratory Technician** show high variation in satisfaction
* Helps identify areas needing improvement

---

## 💻 SQL Queries Used

### 🔹 Department-wise Attrition

```sql id="q1sql"
SELECT department, COUNT(attrition)
FROM hrdata
WHERE attrition = 'Yes'
GROUP BY department
ORDER BY COUNT(attrition) DESC;
```

### 🔹 Female Attrition Percentage

```sql id="q2sql"
SELECT department,
COUNT(attrition),
ROUND((CAST(COUNT(attrition) AS NUMERIC) /
(SELECT COUNT(attrition) FROM hrdata 
 WHERE attrition='Yes' AND gender='Female'))*100,2) AS pct
FROM hrdata
WHERE attrition='Yes' AND gender='Female'
GROUP BY department
ORDER BY COUNT(attrition) DESC;
```

### 🔹 Job Satisfaction Crosstab

```sql id="q3sql"
CREATE EXTENSION IF NOT EXISTS tablefunc;

SELECT *
FROM crosstab(
'SELECT job_role, job_satisfaction, SUM(employee_count)
 FROM hrdata
 GROUP BY job_role, job_satisfaction
 ORDER BY job_role, job_satisfaction'
) AS ct(job_role varchar(50), one numeric, two numeric, three numeric, four numeric)
ORDER BY job_role;
```

---

## 📸 Query Results

<img width="1337" height="953" alt="Screenshot 2026-03-23 133010" src="https://github.com/user-attachments/assets/ed180c87-9b3e-4ff0-9abf-bf916de96905" />

<img width="1506" height="1007" alt="Screenshot 2026-03-23 134931" src="https://github.com/user-attachments/assets/f2709b97-0a3d-4955-bdf8-9c799e2ffe6f" />

<img width="1436" height="977" alt="Screenshot 2026-03-23 140442" src="https://github.com/user-attachments/assets/a64bf040-488d-4e55-8ff0-b9086e4f3851" />

🚀 How to Run

1. Open PostgreSQL / pgAdmin
2. Load dataset into database
3. Run queries from `.sql` file

---

## 💡 Conclusion

This project demonstrates how SQL can be used to analyze HR data and uncover actionable insights. It highlights attrition patterns, gender-based trends, and job satisfaction distribution to support better HR decision-making.


