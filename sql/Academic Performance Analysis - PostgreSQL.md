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

![ERD](docs/ERD_diagram.png)  
> _Add your ERD image to `docs/ERD_diagram.png` and link it here._

---

## 🗝️ **Key Queries & Insights**

### 📌 1. Number of courses offered per department
```sql
SELECT 
  d.department_id,
  d.department_name,
  COUNT(c.course_id) AS number_of_courses
FROM 
  courses c
JOIN 
  departments d ON d.department_id = c.department_id
GROUP BY 
  d.department_id, d.department_name
ORDER BY 
  number_of_courses DESC;
