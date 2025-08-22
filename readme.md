
***

# 🛒 Grocery Store Management Database

## 📌 Overview
The **Grocery Store Management System** is a relational database designed to manage the operations of a grocery store efficiently.  
It provides structured storage for **suppliers, categories, employees, customers, products, orders, and order details**.  

Additionally, it includes **SQL queries for business insights**, allowing analysis of sales, customer engagement, supplier performance, and employee productivity.

***

## 📂 Database Schema

### **1. Supplier Table**
Stores information about suppliers who provide products.  
```sql
CREATE TABLE supplier (
    sup_id TINYINT PRIMARY KEY,
    sup_name VARCHAR(255),
    address TEXT
);
```

### **2. Categories Table**
Stores product categories (e.g., Beverages, Dairy, Snacks).  
```sql
CREATE TABLE categories (
    cat_id TINYINT PRIMARY KEY,
    cat_name VARCHAR(255)
);
```

### **3. Employees Table**
Stores employees who handle customer orders.  
```sql
CREATE TABLE employees (
    emp_id TINYINT PRIMARY KEY,
    emp_name VARCHAR(255),
    hire_date VARCHAR(255)
);
```

### **4. Customers Table**
Stores customer details.  
```sql
CREATE TABLE customers (
    cust_id SMALLINT PRIMARY KEY,
    cust_name VARCHAR(255),
    address TEXT
);
```

### **5. Products Table**
Stores products with relations to suppliers & categories.  
```sql
CREATE TABLE products (
    prod_id TINYINT PRIMARY KEY,
    prod_name VARCHAR(255),
    sup_id TINYINT,
    cat_id TINYINT,
    price DECIMAL(10,2),
    FOREIGN KEY (sup_id) REFERENCES supplier(sup_id)
        ON UPDATE CASCADE ON DELETE CASCADE,
    FOREIGN KEY (cat_id) REFERENCES categories(cat_id)
        ON UPDATE CASCADE ON DELETE CASCADE
);
```

### **6. Orders Table**
Stores customer orders processed by employees.  
```sql
CREATE TABLE orders (
    ord_id SMALLINT PRIMARY KEY,
    cust_id SMALLINT,
    emp_id TINYINT,
    order_date VARCHAR(255),
    FOREIGN KEY (cust_id) REFERENCES customers(cust_id)
        ON UPDATE CASCADE ON DELETE CASCADE,
    FOREIGN KEY (emp_id) REFERENCES employees(emp_id)
        ON UPDATE CASCADE ON DELETE CASCADE
);
```

### **7. Order_Details Table**
Stores details of each product within an order.  
```sql
CREATE TABLE order_details (
    ord_detID SMALLINT AUTO_INCREMENT PRIMARY KEY,
    ord_id SMALLINT,
    prod_id TINYINT,
    quantity TINYINT,
    each_price DECIMAL(10,2),
    total_price DECIMAL(10,2),
    FOREIGN KEY (ord_id) REFERENCES orders(ord_id)
        ON UPDATE CASCADE ON DELETE CASCADE,
    FOREIGN KEY (prod_id) REFERENCES products(prod_id)
        ON UPDATE CASCADE ON DELETE CASCADE
);
```

***

## 📊 Data Analysis Queries

This database includes several **analysis queries for business insights**:

### **1. Customer Insights**
- Unique customers who placed orders  
- Top customers by number of orders  
- Total and average purchase per customer  
- Top 5 customers by total purchase amount  

### **2. Product Performance**
- Products per category  
- Average price by category  
- Best-selling products (by quantity & revenue)  
- Supplier and category-wise sales performance  

### **3. Sales and Order Trends**
- Total orders placed  
- Average order value  
- Dates with most orders  
- Monthly revenue trends  
- Weekday vs weekend orders  

### **4. Supplier Contribution**
- Number of suppliers  
- Supplier with most products  
- Average price per supplier  
- Top supplier by revenue contribution  

### **5. Employee Performance**
- Employees handling most orders  
- Total revenue processed by each employee  
- Average order value handled per employee  

### **6. Order Details Deep Dive**
- Relationship between quantity & total price  
- Average product quantity per order  
- Unit price variations across products and orders  

***

## 🚀 Setup & Usage

1. **Create the database**
```sql
CREATE DATABASE Grocery_Store_Managment;
USE Grocery_Store_Managment;
```

2. **Run the schema script**
Paste the provided SQL schema (`supplier`, `categories`, `employees`, etc.) into your SQL editor to create tables.

3. **Insert sample data** (not included here – add according to your store’s records).

4. **Run analysis queries**  
To generate business insights, use the provided SQL queries.

***

## ✅ Example Queries & Insights

- **Top 5 Customers by Purchase Amount**
```sql
SELECT c.cust_name, SUM(od.total_price) AS total_spent
FROM customers c
JOIN orders o ON c.cust_id=o.cust_id
JOIN order_details od ON o.ord_id=od.ord_id
GROUP BY c.cust_name
ORDER BY total_spent DESC
LIMIT 5;
```

- **Monthly Revenue Trend**
```sql
SELECT DATE_FORMAT(o.order_date, '%Y-%m') AS month,
       SUM(od.total_price) AS monthly_revenue
FROM orders o
JOIN order_details od ON o.ord_id = od.ord_id
GROUP BY month
ORDER BY month;
```

***

## 📌 Future Enhancements
- Add **inventory management** (stock in/out).  
- Track **supplier delivery performance**.  
- Implement **customer loyalty program**.  
- Create **reports dashboard** using BI tools like Power BI / Tableau.  

***

## 🧑💻 Author
📌 **Database Design & Analytics** – Grocery Store Management System  

***
