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
