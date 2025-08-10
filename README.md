# 📊 Data Analyst Internship – Task 4: SQL Analysis on Olist E-Commerce Dataset

## 📌 Overview
This repository contains the work completed for **Task 4** of the **Data Analyst Internship at Elevate Labs**.  
The task involved performing **SQL analysis** on the **Olist Brazilian E-Commerce Public Dataset** using **SQLite**.

**Key activities included:**
- Exploring the dataset  
- Writing queries with **aggregates, joins, subqueries, views, and basic optimization**  
- Generating insights on **customer behavior, sales, and reviews**  

The analysis was conducted in the **SQLite command-line tool** on the `olist.sqlite` database.  
Results and queries are documented here, with references to **screenshots** and a **compiled report**.

---

## 📂 Dataset
**Source:** [Olist Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  

**Tables include:**
- customers  
- orders  
- order_items  
- order_reviews  
- products  
- sellers  
- product_category_name_translation  
- and more  

**File:** `olist.sqlite` *(not included here due to size; download from official sources)*  

**Key Stats (from analysis):**
- ~99,441 orders  
- ~32,951 products  
- ~96,000 unique customers  

---

## ⚙️ Setup and Installation

### **Prerequisites**
- SQLite installed ([Download here](https://sqlite.org/download.html))  
- Python (optional, for scripting or automation)  

### **Clone the Repository**
```bash
git clone https://github.com/yourusername/task4-sql-analysis.git
cd task4-sql-analysis
```

### **Open the Database
Place olist.sqlite in the repo folder.

## Launch SQLite:
```bash
sqlite3 olist.sqlite
```
Run .tables to verify database tables.

🛠 Usage
All queries can be run in the SQLite shell after opening the database.

💡 To save query outputs:

.output "results.txt"
To reset output:
.output

📊 Example Queries
1️⃣ Total Orders by Status
```bash
SELECT order_status, COUNT(*) AS count 
FROM orders 
GROUP BY order_status 
ORDER BY count DESC;
```
2️⃣ Top 10 Cities by Unique Customers
```bash
SELECT customer_city, COUNT(customer_unique_id) AS total_customers 
FROM customers 
GROUP BY customer_city 
ORDER BY total_customers DESC 
LIMIT 10;
```
3️⃣ Top 5 Products by Sales Volume
```bash
SELECT products.product_id, product_category_name_english, COUNT(order_items.order_item_id) AS units_sold 
FROM products 
JOIN order_items ON products.product_id = order_items.product_id 
JOIN product_category_name_translation 
  ON products.product_category_name = product_category_name_translation.product_category_name 
GROUP BY products.product_id 
ORDER BY units_sold DESC 
LIMIT 5;
```
4️⃣ Repeat Customers View
```bash
CREATE VIEW repeat_customers AS 
SELECT customer_unique_id, COUNT(order_id) AS order_count 
FROM customers 
JOIN orders ON customers.customer_id = orders.customer_id 
GROUP BY customer_unique_id 
HAVING order_count > 1;
SELECT * FROM repeat_customers LIMIT 10;
```
5️⃣ Best Performing Categories by Average Review Score
```bash
SELECT p.product_category_name, AVG(r.review_score) AS avg_score
FROM products p
JOIN order_items oi ON p.product_id = oi.product_id
JOIN order_reviews r ON oi.order_id = r.order_id
GROUP BY p.product_category_name
ORDER BY avg_score DESC
LIMIT 5;
```

📈 Results and Insights
Customer Distribution: São Paulo leads with ~15,540 unique customers.

Order Fulfillment: ~97% of orders are delivered.

Top Categories: Health & beauty products sell the most; books and children's fashion receive the highest review scores (~4.4–4.6).

Loyalty: A small number of customers place 10+ orders, showing strong repeat business potential.

📎 Detailed results are available in the screenshots folder and the compiled report.

📄 Report
The full report summarizing queries, results, explanations, and recommendations is available as:
report.md
Includes all referenced screenshots and detailed insights.

📜 License
This project is for educational purposes and uses public dataset sources.
Please credit Olist/Kaggle when using the data.

📬 Contact
If you have questions or suggestions, feel free to:Open an issue in this repository
Contact via email: [anshuyadav1223334444@gmail.com]
