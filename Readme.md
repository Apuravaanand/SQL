<h1 align="center">SQL Mastery Documentation</h1>

<p align="center">
Complete SQL guide covering database fundamentals, table design, CRUD operations, joins, aggregations, subqueries, transactions, and indexing.
</p>

<hr>

<h2>Table of Contents</h2>

<ul>
<li>1. Introduction to Databases</li>
<li>2. Database Creation</li>
<li>3. Table Creation</li>
<li>4. CRUD Operations</li>
<li>5. Query Filtering</li>
<li>6. Sorting Results</li>
<li>7. Aggregations and GROUP BY</li>
<li>8. SQL Functions</li>
<li>9. Joins</li>
<li>10. Views</li>
<li>11. Subqueries</li>
<li>12. Transactions</li>
<li>13. Indexes</li>
<li>14. Database Modeling</li>
</ul>

<hr>

<h2>1. Introduction to Databases</h2>

<p>A database is an organized collection of data stored electronically for easy access and management.</p>

<pre><code>
Example Table

id | name | course
-------------------
1  | John | CS
2  | Amy  | IT
</code></pre>

<hr>

<h2>2. Database Creation</h2>

<p>Create a new database and select it for use.</p>

<pre><code>
CREATE DATABASE company_db;

USE company_db;
</code></pre>

<hr>

<h2>3. Table Creation</h2>

<p>Tables store structured data in rows and columns.</p>

<pre><code>
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100),
  email VARCHAR(100) UNIQUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
</code></pre>

<hr>

<h2>4. CRUD Operations</h2>

<h3>Create (Insert)</h3>

<pre><code>
INSERT INTO users (name,email)
VALUES ('Apurava','apurava@mail.com');
</code></pre>

<h3>Read (Select)</h3>

<pre><code>
SELECT * FROM users;
</code></pre>

<h3>Update</h3>

<pre><code>
UPDATE users
SET name='Apurava Anand'
WHERE id=1;
</code></pre>

<h3>Delete</h3>

<pre><code>
DELETE FROM users
WHERE id=1;
</code></pre>

<hr>

<h2>5. Query Filtering</h2>

<p>Retrieve specific data using conditions.</p>

<pre><code>
SELECT * FROM users WHERE id=2;

SELECT * FROM users
WHERE name LIKE 'A%';

SELECT * FROM users
WHERE id > 5 AND email LIKE '%mail.com';
</code></pre>

Common Operators

<ul>
<li>= Equal</li>
<li>!= Not equal</li>
<li>&gt; Greater than</li>
<li>&lt; Less than</li>
<li>AND / OR / NOT</li>
</ul>

<hr>

<h2>6. Sorting Results</h2>

<p>Sort query results using ORDER BY.</p>

<pre><code>
SELECT * FROM users
ORDER BY created_at DESC;
</code></pre>

<hr>

<h2>7. Aggregations and GROUP BY</h2>

<p>Aggregate functions perform calculations across rows.</p>

<pre><code>
SELECT COUNT(*) FROM users;

SELECT AVG(price) FROM products;

SELECT SUM(total) FROM orders;

SELECT MIN(price), MAX(price) FROM products;
</code></pre>

<h3>GROUP BY</h3>

<pre><code>
SELECT user_id, COUNT(*) AS total_orders
FROM orders
GROUP BY user_id;
</code></pre>

<hr>

<h2>8. SQL Functions</h2>

<p>Functions operate on data and return results.</p>

<pre><code>
SELECT UPPER(name) FROM users;

SELECT LENGTH(name) FROM users;

SELECT NOW();
</code></pre>

<hr>

<h2>9. Joins</h2>

<p>Joins combine data from multiple tables.</p>

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

<h3>FULL JOIN</h3>

<pre><code>
SELECT users.name, orders.total
FROM users
FULL OUTER JOIN orders
ON users.id = orders.user_id;
</code></pre>

<h3>CROSS JOIN</h3>

<pre><code>
SELECT *
FROM users
CROSS JOIN products;
</code></pre>

<hr>

<h2>10. Views</h2>

<p>A view is a virtual table created from a query.</p>

<pre><code>
CREATE VIEW high_value_orders AS
SELECT user_id,total
FROM orders
WHERE total > 50000;
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

<h2>12. Transactions</h2>

<p>Transactions ensure multiple queries execute safely as a single unit.</p>

<pre><code>
BEGIN;

UPDATE users SET balance=balance-100 WHERE id=1;

UPDATE users SET balance=balance+100 WHERE id=2;

COMMIT;
</code></pre>

<hr>

<h2>13. Indexes</h2>

<p>Indexes improve database query performance.</p>

<pre><code>
CREATE INDEX idx_users_email
ON users(email);
</code></pre>

<hr>

<h2>14. Database Modeling</h2>

<p>Database modeling defines relationships between tables.</p>

<pre><code>
Users
------
id
name

Orders
------
id
user_id
total
</code></pre>

Relationship

Users (1) ---- (Many) Orders

<hr>

<p align="center">
SQL Mastery Documentation
</p>
