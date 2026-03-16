<h1>SQL Mastery Cheatsheet for Full-Stack / Web Developers</h1>

<p>This guide contains a complete SQL mastery reference including database creation, table setup, CRUD, joins, aggregations, advanced queries, transactions, indexing, security, and 50 practice questions for hands-on learning.</p>

<hr>

<div class="section">
<h2>Database Creation</h2>
<p>A database is a structured collection of data.</p>
<pre><code>CREATE DATABASE web_app_db;
USE web_app_db;</code></pre>
</div>

<div class="section">
<h2>Table Creation</h2>
<p>Define tables with columns, data types, and constraints.</p>
<pre><code>CREATE TABLE users (
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
);</code></pre>
</div>

<div class="section">
<h2>Insert Data</h2>
<pre><code>INSERT INTO users (name,email,password_hash) VALUES
('Apurava','apurava@mail.com','hashed1'),
('Anand','anand@mail.com','hashed2');

INSERT INTO products (name,price) VALUES
('Laptop',50000),
('Mouse',500);

INSERT INTO orders (user_id,total,status) VALUES
(1,50000,'pending'),
(2,50500,'completed');</code></pre>
</div>

<div class="section">
<h2>Select & Filtering</h2>
<pre><code>SELECT * FROM users;
SELECT name,email FROM users;
SELECT * FROM users WHERE id=1;
SELECT * FROM users WHERE id>1 AND email LIKE '%mail.com';
SELECT * FROM products WHERE price BETWEEN 100 AND 100000;
SELECT * FROM orders WHERE status IN ('pending','completed');</code></pre>
</div>

<div class="section">
<h2>Sorting & Pagination</h2>
<pre><code>SELECT * FROM users ORDER BY created_at DESC;
SELECT * FROM products ORDER BY price ASC LIMIT 5 OFFSET 0;</code></pre>
</div>

<div class="section">
<h2>Aggregation</h2>
<pre><code>SELECT COUNT(*) FROM users;
SELECT SUM(total) FROM orders;
SELECT AVG(price) FROM products;
SELECT MIN(price) FROM products;
SELECT MAX(total) FROM orders;

SELECT user_id, COUNT(*) AS total_orders
FROM orders
GROUP BY user_id
HAVING COUNT(*)>0;</code></pre>
</div>

<div class="section">
<h2>Joins</h2>
<pre><code>-- INNER JOIN
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
FULL OUTER JOIN orders ON users.id = orders.user_id;</code></pre>
</div>

<div class="section">
<h2>Subqueries & EXISTS</h2>
<pre><code>SELECT name FROM users WHERE id IN (SELECT user_id FROM orders WHERE total>50000);
SELECT name FROM users u WHERE EXISTS (SELECT * FROM orders o WHERE u.id=o.user_id);</code></pre>
</div>

<div class="section">
<h2>CASE Statements</h2>
<pre><code>SELECT name,
CASE WHEN total>=50000 THEN 'VIP'
ELSE 'Regular'
END AS customer_type
FROM users
INNER JOIN orders ON users.id=orders.user_id;</code></pre>
</div>

<div class="section">
<h2>Window Functions</h2>
<pre><code>SELECT name, ROW_NUMBER() OVER(ORDER BY created_at DESC) AS row_num
FROM users;

SELECT name, RANK() OVER(ORDER BY created_at DESC) AS rank_num
FROM users;

SELECT name, DENSE_RANK() OVER(ORDER BY created_at DESC) AS dense_rank_num
FROM users;</code></pre>
</div>

<div class="section">
<h2>CTE (Common Table Expression)</h2>
<pre><code>WITH recent_orders AS (
  SELECT * FROM orders WHERE created_at >= NOW() - INTERVAL 7 DAY
)
SELECT * FROM recent_orders;</code></pre>
</div>

<div class="section">
<h2>UNION</h2>
<pre><code>SELECT name FROM users
UNION
SELECT name FROM admins;</code></pre>
</div>

<div class="section">
<h2>Update & Delete</h2>
<pre><code>UPDATE users SET name='Apurava Anand' WHERE id=1;
DELETE FROM orders WHERE status='pending';</code></pre>
</div>

<div class="section">
<h2>Indexing</h2>
<pre><code>CREATE INDEX idx_users_email ON users(email);</code></pre>
</div>

<div class="section">
<h2>Transactions</h2>
<pre><code>BEGIN;
UPDATE users SET balance=balance-100 WHERE id=1;
UPDATE users SET balance=balance+100 WHERE id=2;
COMMIT;</code></pre>
</div>

<div class="section">
<h2>Security / Prevent SQL Injection</h2>
<p>Always use <strong>parameterized queries</strong> in backend frameworks like Node.js, Python, PHP. Never concatenate user input directly.</p>
</div>

<div class="section">
<h2>SQL Practice Questions (50)</h2>
<ol>
  <li>Create a database called <code>web_app_db</code>.</li>
  <li>Create a table <code>users</code> with id, name, email, password, created_at.</li>
  <li>Insert 5 users into <code>users</code>.</li>
  <li>Select all columns from <code>users</code>.</li>
  <li>Select only <code>name</code> and <code>email</code>.</li>
  <li>Update name of user with id=2.</li>
  <li>Delete user with id=5.</li>
  <li>Filter users with age &gt; 25.</li>
  <li>Filter users with name starting with 'A'.</li>
  <li>Select unique ages.</li>
  <li>Select all users ordered by <code>created_at</code> descending.</li>
  <li>Select first 5 users using <code>LIMIT</code>.</li>
  <li>Skip first 10 users, fetch next 5.</li>
  <li>Select products ordered by price ascending.</li>
  <li>Fetch last 10 orders by <code>created_at</code>.</li>
  <li>Count total users.</li>
  <li>Average age of users.</li>
  <li>Sum of all order totals.</li>
  <li>Minimum and maximum product price.</li>
  <li>Count orders per user.</li>
  <li>Count users grouped by city.</li>
  <li>Users with more than 2 orders (HAVING).</li>
  <li>Total sales per product.</li>
  <li>Number of products per category.</li>
  <li>Average order total per month.</li>
  <li>Users in 'Delhi' or 'Mumbai'.</li>
  <li>Products with price 500–5000.</li>
  <li>Users created in last 7 days.</li>
  <li>Users with age&gt;25 or city='Delhi'.</li>
  <li>Orders not 'completed'.</li>
  <li>User names with order totals (INNER JOIN).</li>
  <li>Users with orders, including users without orders (LEFT JOIN).</li>
  <li>Orders including orders without users (RIGHT JOIN).</li>
  <li>Products with category names (INNER JOIN).</li>
  <li>Count total orders per user.</li>
  <li>User names with products they ordered (JOIN multiple tables).</li>
  <li>Users and orders with FULL OUTER JOIN.</li>
  <li>Users with orders &gt; 5000.</li>
  <li>Products never ordered.</li>
  <li>Users with orders (EXISTS).</li>
  <li>Orders above average total (subquery).</li>
  <li>Users enrolled in a course (nested query).</li>
  <li>Mark users as 'VIP' if total purchase &gt;=50,000 else 'Regular'.</li>
  <li>Categorize products as 'Expensive', 'Moderate', 'Cheap'.</li>
  <li>Mark 'New' for users signed up in last 7 days.</li>
  <li>Row numbers to users by signup date.</li>
  <li>Rank users by total order value (RANK()).</li>
  <li>Dense rank users by number of orders.</li>
  <li>CTE: recent orders in last 30 days.</li>
  <li>CTE: total order value per user &gt;50,000.</li>
</ol>
</div>

</body>
</html>