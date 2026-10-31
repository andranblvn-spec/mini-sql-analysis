# mini-sql-analysis
Mini analisa terkait thelook ecommerce di big query
# 🛒 TheLook E-commerce — SQL Analysis

## 📌 Project Overview

This mini project analyzes **TheLook E-commerce** data using **SQL in Google BigQuery**.

The analysis focuses on answering several business questions related to product characteristics, premium product identification, product category distribution, customer orders, and sales performance.

The project demonstrates fundamental SQL skills including:

- `SELECT`
- `WHERE`
- `ORDER BY`
- `GROUP BY`
- Aggregate functions (`COUNT`, `SUM`)
- `JOIN`
- Table aliases

---

## 🗂️ Dataset

**Dataset:** `bigquery-public-data.thelook_ecommerce`

TheLook E-commerce is a public dataset available in Google BigQuery containing simulated e-commerce data.

### Tables Used

| Table | Description |
|---|---|
| `products` | Product information including category, department, brand, and retail price |
| `users` | Customer information and profiles |
| `order_items` | Individual items included in customer orders and their sale prices |

---

## 🔎 Business Questions & Analysis

### 1. Product Analysis

**Business Question:**  
The Product team wants to understand the characteristics of products available in the store.

The analysis retrieves the product name, category, department, brand, and retail price for the first 20 products.

```sql
SELECT
  name,
  category,
  department,
  brand,
  retail_price
FROM
  `bigquery-public-data.thelook_ecommerce.products`
LIMIT 20;
```

---

### 2. Premium Product Identification

**Business Question:**  
The Marketing team wants to prepare a campaign targeting premium products.

Products with a retail price above **$100** are identified and ranked from the highest to the lowest retail price.

```sql
SELECT
  name,
  category,
  department,
  brand,
  retail_price
FROM
  `bigquery-public-data.thelook_ecommerce.products`
WHERE retail_price > 100
ORDER BY retail_price DESC;
```

**Business Use:**  
The result can help the Marketing team identify products that may be suitable for premium campaigns, targeted promotions, or high-value customer segments.

---

### 3. Product Category Evaluation

**Business Question:**  
Which product categories contain the largest number of products?

The number of products in each category is calculated and ranked from highest to lowest.

```sql
SELECT
  category,
  COUNT(id) AS total_products
FROM
  `bigquery-public-data.thelook_ecommerce.products`
GROUP BY category
ORDER BY total_products DESC;
```

### 💡 Insight

- **Intimates** has the largest product assortment with **2,363 products**.
- **Clothing Sets** has the smallest product assortment with only **37 products**.

This indicates that the product catalog is distributed unevenly across categories, with substantially more product variety available in categories such as Intimates.

---

### 4. Customer Order Analysis

**Business Question:**  
The CRM team wants to identify customers who placed orders and review their order information.

Customer information is combined with order item data to display the customer's name, order ID, order status, and order creation date.

```sql
SELECT
  u.first_name,
  u.last_name,
  oi.order_id,
  oi.status,
  oi.created_at AS order_date
FROM
  `bigquery-public-data.thelook_ecommerce.order_items` AS oi
JOIN
  `bigquery-public-data.thelook_ecommerce.users` AS u
  ON oi.user_id = u.id;
```

**Business Use:**  
This analysis allows the CRM team to connect transaction activity with customer information and can serve as a foundation for further customer behavior analysis.

---

### 5. Sales Performance by Category

**Business Question:**  
Which product categories generate the highest sales value?

The `order_items` and `products` tables are joined to calculate total sales value by product category using `sale_price`.

```sql
SELECT
  p.category,
  SUM(oi.sale_price) AS total_revenue
FROM
  `bigquery-public-data.thelook_ecommerce.order_items` AS oi
JOIN
  `bigquery-public-data.thelook_ecommerce.products` AS p
  ON oi.product_id = p.id
GROUP BY p.category
ORDER BY total_revenue DESC;
```

### 💡 Insight

- **Outerwear & Coats** generates the highest total sales value at approximately **$1,324,934.13**.
- **Clothing Sets** generates the lowest total sales value at approximately **$16,631.51**.

Interestingly, the category with the largest number of products is not necessarily the category generating the highest sales value.

---

## 📊 Key Business Insights

### Product Assortment vs. Sales Performance

**Intimates** has the largest product assortment with 2,363 products, while **Outerwear & Coats** generates the highest sales value.

This suggests that having more products in a category does not automatically result in higher sales performance.

### Premium Product Opportunities

Products priced above $100 can be used as a starting point for identifying premium product segments.

The Marketing team could further combine premium product data with historical sales performance to determine which high-value products or categories have the strongest potential for targeted campaigns.

### Category Performance

**Clothing Sets** has both the smallest product assortment and the lowest total sales value among the analyzed categories.

Further analysis could investigate whether this is caused by limited product availability, lower customer demand, pricing, or other factors.

---

## 🛠️ Tools & Technologies

- **Google BigQuery**
- **SQL**
- **GitHub**

---

## 🧠 SQL Concepts Demonstrated

This project demonstrates the use of:

```text
SELECT
FROM
WHERE
ORDER BY
GROUP BY
COUNT()
SUM()
JOIN
ON
Table Aliases
```

These techniques are used to transform raw e-commerce data into information that can support Product, Marketing, CRM, and business decision-making.

---

## 🚀 Potential Further Analysis

This project can be expanded with additional analyses such as:

- Monthly revenue trends
- Top-selling products
- Average Order Value (AOV)
- Customer purchase frequency
- Repeat customer analysis
- Revenue by department
- Revenue by brand
- Order status distribution
- Customer segmentation
- Product price vs. sales performance

---

## 📁 Repository Structure

```text
mini-sql-analysis/
│
├── README.md
└── analysis.sql
```

`analysis.sql` contains the SQL queries used throughout this project.

---
