# plsql-window-functions-IRADUKUNDA-Marie-Sandrine
Milk Delivery Company
# Milk Delivery Company – Window Functions Project  
**Student:** IRADUKUNDA Marie Sandrine  
**ID:** 28327  
**Course:Database Development with PL/SQL   – AUCA  
**Instructor:** Mr. Eric Maniraguha  

---

## 📌 1. Problem Definition
**Business Context:**  
A milk delivery company distributes fresh and processed milk to households, shops, and schools across multiple regions.  

**Data Challenge:**  
The company struggles to track liters sold each month by region and customer type. It is difficult to identify top customers and to monitor changes in sales over time. This creates risks such as poor demand forecasting, stock shortages, and missed opportunities to reward loyal customers.  

**Expected Outcome:**  
Reports that highlight top 5 customers per region, monthly running totals, month-over-month growth, and customer quartile segmentation for targeted loyalty programs.

---

## 🎯 2. Success Criteria
The project will be successful if it achieves these **five measurable goals**:  
1. Identify **Top 5 customers per region by liters delivered** using `RANK()` or `ROW_NUMBER()`.  
2. Compute **running monthly totals** of liters sold using `SUM() OVER (ORDER BY ...)`.  
3. Calculate **month-over-month growth** in liters with `LAG()`.  
4. Segment customers into **quartiles** with `NTILE(4)`.  
5. Calculate a **3-month moving average** of liters delivered using `AVG() OVER (...)`.  

---

## 🗄️ 3. Database Schema

### Tables
**Customers**
```sql
CREATE TABLE customers (
  customer_id  NUMBER PRIMARY KEY,
  name         VARCHAR2(100),
  region       VARCHAR2(50)
);
```
Products
```sql
CREATE TABLE products (
  product_id   NUMBER PRIMARY KEY,
  name         VARCHAR2(100),
  category     VARCHAR2(50)
);
```
DELIVERIES
```sql
CREATE TABLE deliveries (
  delivery_id    NUMBER PRIMARY KEY,
  transaction_id NUMBER REFERENCES transactions(transaction_id),
  delivery_date  DATE,
  status         VARCHAR2(20)
);
```
Sample data
customers
```sql
INSERT INTO customers VALUES (1, 'Alice Uwase', 'Kigali');
INSERT INTO customers VALUES (2, 'John Niyonsenga', 'Musanze');
INSERT INTO customers VALUES (3, 'Grace Mukamana', 'Huye');
INSERT INTO customers VALUES (4, 'Eric Habimana', 'Rubavu');
```
products
```sql
INSERT INTO products VALUES (101, 'Coffee Beans', 'Beverage');
INSERT INTO products VALUES (102, 'Tea Pack', 'Beverage');
INSERT INTO products VALUES (103, 'Milk Carton', 'Dairy');
INSERT INTO products VALUES (104, 'Chocolate Bar', 'Snack');
```
deliveries
```sql
INSERT INTO deliveries VALUES (201, 1001, DATE '2025-09-02', 'Delivered');
INSERT INTO deliveries VALUES (202, 1002, DATE '2025-09-06', 'Pending');
INSERT INTO deliveries VALUES (203, 1003, DATE '2025-09-11', 'Delivered');
INSERT INTO deliveries VALUES (204, 1004, DATE '2025-09-16', 'In Transit');
```
💻 4. Window Functions Implementation
1) Ranking Functions
```sql
SELECT customer_id,
       SUM(amount) AS total_amount,
       ROW_NUMBER() OVER (ORDER BY SUM(amount) DESC) AS row_num,
       RANK() OVER (ORDER BY SUM(amount) DESC) AS rank_num,
       DENSE_RANK() OVER (ORDER BY SUM(amount) DESC) AS dense_rank_num
FROM deliveries
GROUP BY customer_id
ORDER BY total_amount DESC;
...Interpretation:

ROW_NUMBER gives a strict order (no ties).

RANK leaves gaps if there are ties.

DENSE_RANK doesn’t leave gaps.
```
