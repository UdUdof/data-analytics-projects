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
<p align="center">
  <img src="docs/TopServEmp.png" alt="Top Serving Employees" width="650">
</p>
The image displays the top five longest-serving employees at NextGen Corp., based on their hire dates.

---
 b) What is the turnover rate for each department?
 ####
   This section looks at how many employees are leaving each department. A high turnover rate in a department could mean there are      issues like **poor work environment, low satisfaction, or lack of support**.
   
  I calculated the turnover rate using this formula:
   
            Turnover Rate (%) = (Number of Employees Who Left / Total Employees in Department) * 100

  ```sql
   SELECT 
		d.department_id, 
		d.department_name, 
        ROUND((CAST(COUNT(t.employee_id) AS DECIMAL) / COUNT(e.employee_id) * 100),2) AS "Turnover Rate"
	FROM department d
    JOIN employee e ON d.department_id = e.department_id
	LEFT JOIN turnover t ON e.employee_id = t.employee_id
	GROUP BY d.department_id, d.department_name;
   ```
Results:

  <img src="docs/TurnOverRate.png" alt="Turn Over Rate" width="400"> 
  
Visualization:  
  <img src="docs/TOR.png" alt="Turn Over Rate" width="450">

**Key Insights**
- Marketing has the highest turnover rate at 92.86%, suggesting a possible issue with retention in that department.
- Engineering also shows a relatively high turnover rate of 66.67%, which may warrant further investigation.
- Sales and HR have significantly lower turnover rates at 27.59% and 27.27% respectively, indicating better employee stability in those areas.

---
c) Which employees are at risk of leaving based on their performance?
 ####
   Employees with consistently low or declining performance and engagement are more likely to leave. Identifying them early allows    management to offer support and improve retention.
   
  ```sql
   SELECT e.employee_id, 
		   e.first_name,
		   e.last_name,
		   p.performance_score,
		   t.turnover_date
	FROM employee e
   LEFT JOIN performance p ON e.employee_id = p.employee_id
   LEFT JOIN turnover t ON e.employee_id = t.employee_id
   WHERE  p.performance_score <= 3.5 AND turnover_date IS NULL -- they still work at the company
   ORDER BY p.performance_score ASC;
   ```
Results:

  <img src="docs/RiskOfLevn.png" width="550"> 

---
d) What are the main reasons employees are leaving the company?
 ####
   Employees often leave due to factors like lack of growth opportunities, poor management, inadequate compensation, work-life          imbalance, and low job satisfaction. Identifying these causes helps the company address issues and improve retention.
   
  ```sql
   SELECT reason_for_leaving,
	COUNT(employee_id) AS "Total Leave"
	FROM turnover
	GROUP BY reason_for_leaving
	ORDER BY "Total Leave" DESC;
   ```
Results:

  <img src="docs/ResnLeav.png" width="290"> 
  
Visualization:  
  <img src="docs/LeavRsnn.png" width="450">

---
