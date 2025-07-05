# 🗂️ Lewis Office Stationery & Decors — Business Performance Analysis

This project analyzes sales and product performance for **Lewis Office Stationery & Decors**, a supplier of office supplies, furnishings, housekeeping equipment, and public area items to various properties in the USA.

The data is stored in a **PostgreSQL database** with three main tables:
- **orders** — contains order transactions
- **products** — contains product details, including prices and categories
- **propertyinfo** — contains property details, including city and state

---

## 🏢 **Business Context**

Lewis wants to better understand how the business has performed over time and has provided raw data in SQL format. The goal is to answer key questions to inform revenue optimization, product performance, and future business decisions.

---

## 🗃️ **Database Structure**

| Table         | Description                                                   |
|---------------|----------------------------------------------------------------|
| `orders`      | Records each order placed, including order IDs, product IDs, property IDs, order date and quantities. |
| `products`    | Contains product information such as name, category, and price. |
| `propertyinfo`| Holds details about the properties ordering products, including city and state. |

---

## 📊 **Questions Answered**

### 1. Revenue by Product Category (with Conditional Discounts)

> **Business Rule:**  
> - Products costing **> $100** get a **10% discount**.  
> - Products costing **$50 – $100** get a **5% discount**.  

```sql
SELECT "ProductCategory", 
  	 	SUM(CASE
           WHEN "Price" > 100 then "Price" * 0.9 * "Quantity" 
  				 WHEN "Price" BETWEEN 50 AND 100 then "Price" * 0.95 * "Quantity" 
  				 ELSE "Price" * "Quantity"
  		END) AS "Discounted Revenue" 
FROM orders
JOIN products on orders."ProductID" = products."ProductID" --JOIN: INNER
GROUP BY "ProductCategory";
```
![ERD Diagram](docs/ERD_diagram.png)
