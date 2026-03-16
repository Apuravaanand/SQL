<h1 align="center">SQL for Full-Stack Developers</h1>

<p align="center">
Structured SQL syllabus and documentation for backend and full-stack development.
Includes database design, CRUD operations, joins, aggregations, advanced queries,
transactions, and optimization techniques.
</p>

<hr>

<h2>Table of Contents</h2>

<ul>
<li>1. Database Fundamentals</li>
<li>2. Database Creation</li>
<li>3. Table Design</li>
<li>4. Constraints</li>
<li>5. CRUD Operations</li>
<li>6. Query Filtering</li>
<li>7. Sorting and Pagination</li>
<li>8. Aggregations</li>
<li>9. SQL Functions</li>
<li>10. Joins</li>
<li>11. Subqueries</li>
<li>12. Views</li>
<li>13. CASE Statements</li>
<li>14. Set Operations</li>
<li>15. Window Functions</li>
<li>16. Common Table Expressions (CTE)</li>
<li>17. Transactions</li>
<li>18. Indexing</li>
<li>19. Database Modeling for Web Apps</li>
<li>20. Security Best Practices</li>
</ul>

<hr>

<h2>1. Database Fundamentals</h2>

<p>
A database is an organized collection of data stored electronically for efficient access and management.
</p>

<table>
<tr>
<th>ID</th>
<th>Name</th>
<th>Email</th>
</tr>
<tr>
<td>1</td>
<td>Apurava</td>
<td>apurava@mail.com</td>
</tr>
<tr>
<td>2</td>
<td>Anand</td>
<td>anand@mail.com</td>
</tr>
</table>

<h3>Types of Databases</h3>

<ul>
<li>Relational Databases (SQL)</li>
<li>NoSQL Databases</li>
<li>Distributed Databases</li>
</ul>

<h3>Popular SQL Databases</h3>

<ul>
<li>MySQL</li>
<li>PostgreSQL</li>
<li>SQLite</li>
<li>SQL Server</li>
</ul>

<hr>

<h2>2. Database Creation</h2>

<p>Create a new database.</p>

<pre><code>
CREATE DATABASE web_app_db;
</code></pre>

<p>Select the database.</p>

<pre><code>
USE web_app_db;
</code></pre>

<p>Delete a database.</p>

<pre><code>
DROP DATABASE web_app_db;
</code></pre>

<hr>

<h2>3. Table Design</h2>

<p>Tables store structured data in rows and columns.</p>

<pre><code>
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100),
  email VARCHAR(100),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
</code></pre>

<hr>

<h2>4. Constraints</h2>

<p>Constraints enforce rules on data in tables.</p>

<ul>
<li>PRIMARY KEY</li>
<li>FOREIGN KEY</li>
<li>UNIQUE</li>
<li>NOT NULL</li>
<li>CHECK</li>
<li>DEFAULT</li>
</ul>

<pre><code>
CREATE TABLE products (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100) NOT NULL,
  price DECIMAL(10,2) CHECK(price > 0),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
</code></pre>

<hr>

<h2>5. CRUD Operations</h2>

<h3>Insert Data</h3>

<pre><code>
INSERT INTO users (name,email)
VALUES ('Apurava','apurava@mail.com');
</code></pre>

<h3>Read Data</h3>

<pre><code>
SELECT * FROM users;
</code></pre>

<h3>Update Data</h3>

<pre><code>
UPDATE users
SET name='Apurava Anand'
WHERE id=1;
</code></pre>

<h3>Delete Data</h3>

<pre><code>
DELETE FROM users
WHERE id=1;
</code></pre>

<hr>

<h2>6. Query Filtering</h2>

<p>Filter records using conditions.</p>

<pre><code>
SELECT * FROM users WHERE id=2;

SELECT * FROM users
WHERE name LIKE 'A%';

SELECT * FROM users
WHERE id > 5 AND email LIKE '%mail.com';
</code></pre>

<h3>Common Operators</h3>

<ul>
<li>= Equal</li>
<li>!= Not Equal</li>
<li>&gt; Greater Than</li>
<li>&lt; Less Than</li>
<li>AND / OR / NOT</li>
<li>IN</li>
<li>BETWEEN</li>
</ul>

<hr>

<h2>7. Sorting and Pagination</h2>

<pre><code>
SELECT * FROM users
ORDER BY created_at DESC;

SELECT * FROM users
LIMIT 10 OFFSET 20;
</code></pre>

<hr>

<h2>8. Aggregations</h2>

<p>Aggregate functions perform calculations across rows.</p>

<pre><code>
SELECT COUNT(*) FROM users;

SELECT SUM(total) FROM orders;

SELECT AVG(price) FROM products;

SELECT MIN(price), MAX(price) FROM products;
</code></pre>

<h3>GROUP BY</h3>

<pre><code>
SELECT user_id, COUNT(*) AS total_orders
FROM orders
GROUP BY user_id;
</code></pre>

<hr>

<h2>9. SQL Functions</h2>

<pre><code>
SELECT UPPER(name) FROM users;

SELECT LENGTH(name) FROM users;

SELECT NOW();
</code></pre>

<hr>

<h2>10. Joins</h2>

<p>Joins combine rows from multiple tables.</p>

<h3>INNER JOIN</h3>

<pre><code>
SELECT users.name, orders.total
FROM users
INNER JOIN orders
ON users.id = orders.user_id;
</code></pre>

<h3>LEFT JOIN</h3>

<pre><code>
SELECT users.name, orders.total
FROM users
LEFT JOIN orders
ON users.id = orders.user_id;
</code></pre>

<h3>RIGHT JOIN</h3>

<pre><code>
SELECT users.name, orders.total
FROM users
RIGHT JOIN orders
ON users.id = orders.user_id;
</code></pre>

<h3>FULL OUTER JOIN</h3>

<pre><code>
SELECT users.name, orders.total
FROM users
FULL OUTER JOIN orders
ON users.id = orders.user_id;
</code></pre>

<hr>

<h2>11. Subqueries</h2>

<p>A subquery is a query nested inside another query.</p>

<pre><code>
SELECT name
FROM users
WHERE id IN (
  SELECT user_id FROM orders
);
</code></pre>

<hr>

<h2>12. Views</h2>

<p>A view is a virtual table created from a query.</p>

<pre><code>
CREATE VIEW high_value_orders AS
SELECT user_id,total
FROM orders
WHERE total > 50000;
</code></pre>

<hr>

<h2>13. CASE Statements</h2>

<pre><code>
SELECT name,
CASE
  WHEN total >= 50000 THEN 'VIP'
  ELSE 'Regular'
END AS customer_type
FROM users
JOIN orders ON users.id = orders.user_id;
</code></pre>

<hr>

<h2>14. Set Operations</h2>

<pre><code>
SELECT name FROM users
UNION
SELECT name FROM admins;
</code></pre>

<hr>

<h2>15. Window Functions</h2>

<pre><code>
SELECT name,
ROW_NUMBER() OVER(ORDER BY created_at DESC)
FROM users;
</code></pre>

<hr>

<h2>16. Common Table Expressions (CTE)</h2>

<pre><code>
WITH recent_orders AS (
  SELECT * FROM orders
  WHERE created_at >= NOW() - INTERVAL 7 DAY
)
SELECT * FROM recent_orders;
</code></pre>

<hr>

<h2>17. Transactions</h2>

<p>Transactions ensure data consistency.</p>

<pre><code>
BEGIN;

UPDATE users SET balance = balance - 100 WHERE id = 1;
UPDATE users SET balance = balance + 100 WHERE id = 2;

COMMIT;
</code></pre>

<hr>

<h2>18. Indexing</h2>

<p>Indexes improve database performance.</p>

<pre><code>
CREATE INDEX idx_users_email
ON users(email);
</code></pre>

<hr>

<h2>19. Database Modeling for Web Apps</h2>

<p>Design relationships between tables.</p>

<pre><code>
Users
-----
id
name

Orders
------
id
user_id
total
</code></pre>

<p>Relationship:</p>

<pre>
Users (1) ---- (Many) Orders
</pre>

<hr>

<h2>20. Security Best Practices</h2>

<ul>
<li>Use parameterized queries</li>
<li>Validate user input</li>
<li>Avoid raw SQL concatenation</li>
<li>Use least-privilege database users</li>
</ul>

<pre><code>
db.query("SELECT * FROM users WHERE email=?", [email]);
</code></pre>

<hr>

<p align="center">
SQL Documentation for Full-Stack Developers
</p>
