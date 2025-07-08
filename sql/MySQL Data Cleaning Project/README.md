# 🧹 MySQL Data Cleaning Project — [Dataset Name]

This project demonstrates **practical data cleaning** using **MySQL**.  
It showcases techniques to check, clean, and transform raw data into a usable format for analysis.

---

## 📊 **Project Overview**

**Context:**  
The dataset includes the names of com dataset was collected shared by Alex The Analyst on Youtube  
It contained common issues such as:
- Inconsistent formatting
- Duplicates
- NULL or missing values
- Outliers and invalid records

**Goal:**  
To apply **SQL data cleaning techniques** so the final dataset is reliable for analysis and reporting.

---

## 🗃️ **Database Structure**

| Table         | Description                                      |
|---------------|--------------------------------------------------|
| `raw_data`    | Original uncleaned data                          |
| `cleaned_data`| Final cleaned version, after transformations     |
| *(Optional)* `lookup_tables` | Reference data for validation (e.g., country codes, valid categories) |

---

## 🧹 **Key Cleaning Steps**

Below are some typical tasks performed with **MySQL queries**.

### ✅ 1. Standardize text formats

```sql
UPDATE raw_data
SET customer_name = TRIM(UPPER(customer_name));
