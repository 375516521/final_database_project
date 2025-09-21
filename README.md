
# E-commerce Database Schema

This project provides a **clean, re-runnable SQL schema** for an e-commerce store.
The schema is written for **MySQL** and includes users, products, categories, orders, payments, carts, coupons, and reviews.

The script uses `DROP TABLE IF EXISTS` before each `CREATE TABLE` so it can be run multiple times without errors.



## 📂 File

* `ecommerce_schema_clean.sql` → SQL script containing the full database schema, constraints, indexes, and sample seed data.


## 🚀 How to Use

### 1. Open MySQL Workbench (or MySQL CLI)

* If using **Workbench** → open a new SQL tab.
* If using **CLI**:

  ```bash
  mysql -u root -p
  

### 2. Run the script

* Copy/paste the contents of `ecommerce_schema_clean.sql` into the SQL editor, or
* Import and run the file directly:

  ```bash
  SOURCE /path/to/ecommerce_schema_clean.sql;
  

### 3. Select the database

```sql
USE ecommerce_db;
SHOW TABLES;




## 🏗️ Schema Overview

### Lookup Tables

* **order\_status** → pending, processing, shipped, delivered, cancelled, refunded
* **payment\_method** → credit card, PayPal, bank transfer, cash on delivery

### Users & Addresses

* `users` → customer accounts
* `addresses` → shipping/billing addresses (supports default address per user)

### Products

* `products` → product catalog (with price, description, SKU)
* `product_images` → product image URLs
* `categories` → hierarchical categories (self-referencing `parent_id`)
* `product_categories` → many-to-many relation between products & categories
* `suppliers` → supplier details
* `supplier_products` → supplier ↔ product relations with cost & lead times
* `inventory` → stock tracking per product

### Carts & Orders

* `carts` and `cart_items` → user shopping carts
* `orders` → customer orders
* `order_items` → line items within an order
* `payments` → payment records linked to orders
* `coupons` and `order_coupons` → discount system

### Reviews

* `reviews` → product reviews (unique per user/product)

### Indexes

* Added for products (`name`, `sku`), orders (`user_id`, `placed_at`), and inventory (`quantity`) to improve query performance.



## 🧪 Sample Data

The schema includes **seed data**:

* Categories: *Electronics*, *Books*, *Home & Kitchen*
* Suppliers: *Acme Supplies Ltd*, *Global Distributors*
* Products:

  * USB-C Charging Cable
  * Stainless Steel Water Bottle
  * Intro to SQL (Paperback)
* Inventory: each product initialized with `quantity = 100`

Verify with:

```sql
USE ecommerce_db;
SELECT * FROM categories;
SELECT * FROM products;
SELECT * FROM inventory;
```



## ✅ Notes

* Database name: **`ecommerce_db`**
* Script is **idempotent** (safe to re-run).
* All tables use **InnoDB** with **UTF8MB4** encoding for international support.
* Foreign keys enforce referential integrity with cascading rules.
