-- ===================================================
<h2>DATABASE CREATION</h2>
<p> A database is a structured collection of data.</p>
-- ===================================================

CREATE DATABASE web_app_db;
USE web_app_db;

-- ===================================================
<h2>TABLE CREATION</h2>
<p>Define table structure with columns, types, and constraints</p>
-- ===================================================

CREATE TABLE users (
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(50) NOT NULL,
email VARCHAR(100) UNIQUE NOT NULL,
password_hash VARCHAR(255) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE products (
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(100),
price DECIMAL(10,2),
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE orders (
id INT PRIMARY KEY AUTO_INCREMENT,
user_id INT,
total DECIMAL(10,2),
status VARCHAR(20),
FOREIGN KEY(user_id) REFERENCES users(id)
);

CREATE TABLE enrollments (
id INT PRIMARY KEY AUTO_INCREMENT,
student_id INT,
course_id INT,
FOREIGN KEY(student_id) REFERENCES users(id)
);

-- ===================================================
<h2>INSERT DATA</h2>
-- ===================================================

INSERT INTO users (name,email,password_hash) VALUES
('Apurava','apurava@mail.com','hashed1'),
('Anand','anand@mail.com','hashed2');

INSERT INTO products (name,price) VALUES
('Laptop',50000),
('Mouse',500);

INSERT INTO orders (user_id,total,status) VALUES
(1,50000,'pending'),
(2,50500,'completed');

-- ===================================================
<h2>SELECT & FILTERING</h2>
-- ===================================================

SELECT * FROM users;
SELECT name,email FROM users;
SELECT * FROM users WHERE id=1;
SELECT * FROM users WHERE id>1 AND email LIKE '%mail.com';
SELECT * FROM products WHERE price BETWEEN 100 AND 100000;
SELECT * FROM orders WHERE status IN ('pending','completed');

-- ===================================================
<h2>SORTING & PAGINATION</h2>
-- ===================================================

SELECT * FROM users ORDER BY created_at DESC;
SELECT * FROM products ORDER BY price ASC LIMIT 5 OFFSET 0;

-- ===================================================
<h2>AGGREGATION</h2>
-- ===================================================

SELECT COUNT(*) FROM users;
SELECT SUM(total) FROM orders;
SELECT AVG(price) FROM products;
SELECT MIN(price) FROM products;
SELECT MAX(total) FROM orders;
SELECT user_id, COUNT(*) AS total_orders
FROM orders
GROUP BY user_id
HAVING COUNT(*)>0;

-- ===================================================
<h2>JOINS</h2>
-- ===================================================

-- INNER JOIN
SELECT users.name, orders.total
FROM users
INNER JOIN orders ON users.id = orders.user_id;

-- LEFT JOIN
SELECT users.name, orders.total
FROM users
LEFT JOIN orders ON users.id = orders.user_id;

-- RIGHT JOIN
SELECT users.name, orders.total
FROM users
RIGHT JOIN orders ON users.id = orders.user_id;

-- FULL JOIN (PostgreSQL)
SELECT users.name, orders.total
FROM users
FULL OUTER JOIN orders ON users.id = orders.user_id;

-- ===================================================
<h2>SUBQUERIES & EXISTS</h2>
-- ===================================================

SELECT name FROM users WHERE id IN (SELECT user_id FROM orders WHERE total>50000);

SELECT name FROM users u WHERE EXISTS (SELECT * FROM orders o WHERE u.id=o.user_id);

-- ===================================================
<h2>CASE STATEMENTS</h2>
-- ===================================================

SELECT name,
CASE WHEN total>=50000 THEN 'VIP'
ELSE 'Regular'
END AS customer_type
FROM users
INNER JOIN orders ON users.id=orders.user_id;

-- ===================================================
<h2>WINDOW FUNCTIONS</h2>
-- ===================================================

SELECT name, ROW_NUMBER() OVER(ORDER BY created_at DESC) AS row_num
FROM users;

SELECT name, RANK() OVER(ORDER BY created_at DESC) AS rank_num
FROM users;

SELECT name, DENSE_RANK() OVER(ORDER BY created_at DESC) AS dense_rank_num
FROM users;

-- ===================================================
<h2>CTE (Common Table Expression)</h2>
-- ===================================================

WITH recent_orders AS (
SELECT * FROM orders WHERE created_at >= NOW() - INTERVAL 7 DAY
)
SELECT * FROM recent_orders;

-- ===================================================
<h2>UNION</h2>
-- ===================================================

SELECT name FROM users UNION
SELECT name FROM admins;

-- ===================================================
<h2>UPDATE & DELETE</h2>
-- ===================================================
UPDATE users SET name='Apurava Anand' WHERE id=1;
DELETE FROM orders WHERE status='pending';

-- ===================================================
<h2>INDEXING</h2>
-- ===================================================
CREATE INDEX idx_users_email ON users(email);

-- ===================================================
<h2>TRANSACTIONS</h2>
-- ===================================================

BEGIN;
UPDATE users SET balance=balance-100 WHERE id=1;
UPDATE users SET balance=balance+100 WHERE id=2;
COMMIT;

-- ===================================================
<h2>SECURITY / PREVENT SQL INJECTION</h2>
-- ===================================================
-- Always use parameterized queries in your backend framework (Node.js, Python, PHP)








SQL Practice Questions for Web/Full-Stack Developers (50 Questions)
1. Basics & CRUD (1–10)

Create a database called web_app_db.

Create a table users with columns: id, name, email, password, created_at.

Insert 5 users into the users table.

Select all columns from users.

Select only name and email from users.

Update the name of a user with id=2.

Delete a user with id=5.

Filter users whose age > 25.

Filter users whose name starts with 'A'.

Select unique ages from users.

2. Sorting & Pagination (11–15)

Select all users ordered by created_at descending.

Select the first 5 users using LIMIT.

Skip the first 10 users and fetch the next 5.

Select products ordered by price ascending.

Fetch the last 10 orders by created_at.

3. Aggregation & Grouping (16–25)

Count total users in the users table.

Find the average age of users.

Find the sum of all order totals.

Find the minimum and maximum product price.

Count orders per user.

Count users grouped by city.

Find users with more than 2 orders (HAVING).

Calculate total sales per product.

Find the number of products in each category.

Calculate average order total per month.

4. Filtering & Conditions (26–30)

Select users whose city is either 'Delhi' or 'Mumbai'.

Select products with price between 500 and 5000.

Select users created in the last 7 days.

Select users who have either age>25 or city='Delhi'.

Select orders where status is not 'completed'.

5. Joins (31–37)

Get all user names with their order totals (INNER JOIN).

Get all users with orders, including users with no orders (LEFT JOIN).

Get all orders including orders without users (RIGHT JOIN).

Get products with their category names (INNER JOIN).

Count total orders per user using JOIN.

Get user names with products they ordered (JOIN multiple tables).

Fetch users and orders with FULL OUTER JOIN (PostgreSQL).

6. Subqueries & EXISTS (38–42)

Select users who have placed orders > 5000.

Select products that have never been ordered.

Use EXISTS to select users who have orders.

Use a subquery to find orders above average total.

Use a nested query to select users who enrolled in a course.

7. CASE & Conditional Queries (43–45)

Mark users as 'VIP' if total purchase >= 50,000 else 'Regular'.

Categorize products as 'Expensive', 'Moderate', 'Cheap' based on price.

Use CASE to show 'New' for users signed up in last 7 days.

8. Window Functions & CTEs (46–50)

Assign row numbers to users ordered by signup date.

Rank users by total order value using RANK().

Dense rank users by number of orders.

Use a CTE to get recent orders in last 30 days.

Use a CTE to calculate total order value per user and filter total>50,000.
