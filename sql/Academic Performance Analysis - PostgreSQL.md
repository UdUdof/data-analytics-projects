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

### 📌 1. Number of courses offered per department
```sql
	SELECT course_name AS "Courses"
	FROM courses;
