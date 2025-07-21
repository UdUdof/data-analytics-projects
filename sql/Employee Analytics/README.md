# 📊 NextGen Corp. Employee Analytics

[![Tool](https://img.shields.io/badge/tool-PostgreSQL-blue?logo=postgresql&logoColor=white)](https://www.postgresql.org/)

---

## 🚀 Project Overview

**NextGen Corp.** is a dynamic technology company specializing in innovative software and hardware solutions. While the company continues to attract top talent and drive growth, recent concerns have emerged around:

- Increasing **employee turnover**
- Variability in **employee performance**
- Salary **disparities** across departments

This project provides a **data-driven HR strategy** to uncover insights, improve employee retention, and ensure equitable compensation practices across the organization.

---

## 🎯 Objectives

- 🔍 Identify trends and patterns in employee **retention** and **turnover**
- 📈 Track and evaluate **performance** across departments
- ⚖️ Assess the relationship between **salary and performance** to ensure fairness and satisfaction

---

## 🗂️ Datasets

| Table         | Description |
|---------------|-------------|
| `employee`    | Basic employee details, hire dates, and department affiliation |
| `department`  | Department names and IDs |
| `performance` | Employee monthly performance scores |
| `salary`      | Salary data,including historical salary information for each employee |
| `turnover`    | Exit dates and reasons for leaving |
| `attendance`  | Attendance logs for employees |

---

### 💻 Tools Used
- PostgreSQL or 
- Microsoft Excel visuals

---

## 📊 Sample Visuals
_(Add screenshots or chart previews here if applicable)_

---

## 📌 Key Insights
  ### 1) Employee Retention Analysis
  a) Who are the top 5 highest serving employees?
  ```sql
   SELECT 
   e.employee_id,
   e.department_id,
   e.first_name,
   e.last_name,
   e.hire_date,
   COALESCE(TO_CHAR(t.turnover_date, 'YYYY-MM-DD'), 'Still employed') AS "Status"
   FROM employee e
   LEFT JOIN turnover t ON e.employee_id = t.employee_id
   LEFT JOIN department d ON t.department_id = d.department_id
   WHERE t.turnover_date IS NULL  
   ORDER BY e.hire_date
   LIMIT 5;
  ```
---

> **NextGen Corp. — Empowering Growth Through People Data**
