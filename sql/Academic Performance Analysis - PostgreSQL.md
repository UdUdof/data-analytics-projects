# 🎓 Academic Performance Analysis — PostgreSQL 

This project analyzes academic data stored in a PostgreSQL database, covering **departments**, **courses**, **teachers**, and **student scores**.  
It demonstrates practical skills in database design, SQL querying, and data insights generation.

---

## 🗃️ **Project Structure**

| Table       | Description                                      |
|-------------|--------------------------------------------------|
| `departments` | List of departments                            |
| `courses`     | Courses offered, linked to departments & scores |
| `teacher`     | Teacher details                                 |
| `scores`      | Student scores per course                      |

---

## 🔗 **Entity-Relationship Diagram (ERD)**

**Entities & relationships:**
- A **department** can offer many **courses**
- A **teacher** can teach many **courses**
- A **course** can have many **scores** (one per student)
- Each **score** ties a student to a course
  
<p align="center">
  <img src="EntityDiagram.png" alt="ERD" width="700" height="200"/>
</p>


---

## 🗝️ **Key Queries & Insights**

### 📌 1. Courses offered per department
```sql
	SELECT course_name AS "Courses"
	FROM courses;
```
<p align="left">
  <img src="coursesOffered.png" alt="courses" width="250" height="50"/>
</p>
Looks like this department is for Data Analytics, awesome!

---

### 📌 2. The departments in the school
```sql
	SELECT department_id, department_name
	FROM departments;
```
<p align="left">
  <img src="dept.png" alt="depts" width="250" height="100"/>
</p>
There're four(4) departments, each focused on the various tools used in Data Analytics

---
### 📌 3. Number of teachers
```sql
	SELECT COUNT(DISTINCT(teacher_id))
	FROM teacher;
```
<p align="left">
  <img src="teachers.png" alt="depts" width="250" height="100"/>
</p>
There's a total of eight(8) teachers in the school

---
### 📌 4. Number of students per department
```sql
	SELECT d.department_id, d.department_name, COUNT(s.student_id) AS "Number of Students"
	FROM scores s
	JOIN 
	  courses c ON s.course_id = c.course_id
	RIGHT JOIN 
	  departments d ON c.department = d.department_id
	  GROUP BY d.department_name, d.department_id;
```
<p align="left">
  <img src="studentsPerDept.png" alt="Studepts" width="250" height="100"/>
</p>
Only departsment 1 and 2 have students taking courses

---
### 📌 5. Number of courses offered in each department
```sql
	SELECT d.department_id, d.department_name, COUNT(s.student_id) AS "Number of Students"
	FROM scores s
	JOIN 
	  courses c ON s.course_id = c.course_id
	RIGHT JOIN 
	  departments d ON c.department = d.department_id
	  GROUP BY d.department_name, d.department_id;
```
<p align="left">
  <img src="studentsPerDept.png" alt="Studepts" width="250" height="100"/>
</p>
Only departments 1 and 2 have students taking courses

---


