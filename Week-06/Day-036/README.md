# 🗄️DAY-36 SQL Fundamentals — TryHackMe

## 📌 Overview

This room introduces the **fundamentals of SQL (Structured Query Language)** and how to interact with **relational databases**. It covers core concepts such as databases, tables, CRUD operations, clauses, operators, and functions. These skills are essential for cybersecurity roles, especially in **web security, pentesting, and data analysis**.

Room: [https://tryhackme.com/room/sqlfundamentals](https://tryhackme.com/room/sqlfundamentals)

---

## 🎯 Learning Objectives

* Understand what databases are and how relational databases work
* Learn basic SQL syntax and commands
* Perform CRUD operations
* Use clauses, operators, and functions to filter and manipulate data
* Build a solid foundation for SQL Injection and database analysis

---

## 🧠 Database Basics

### What is a Database?

A database is an organized collection of structured data that allows efficient storage, retrieval, and manipulation of information.

### Relational Databases

* Data is stored in **tables** (rows and columns)
* Tables can be linked using keys

### Key Concepts

* **Table**: Collection of related data
* **Row (Record)**: Single entry in a table
* **Column (Field)**: Specific attribute of the data
* **Primary Key**: Unique identifier for each record
* **Foreign Key**: Creates relationships between tables

---

## 🛠️ SQL Basics

SQL is used to communicate with a **DBMS** (Database Management System) such as MySQL.

### Common Commands

```sql
SHOW DATABASES;
USE database_name;
SHOW TABLES;
```

---

## 📊 CRUD Operations

CRUD stands for **Create, Read, Update, Delete**.

### CREATE (INSERT)

```sql
INSERT INTO books (id, name, published_date, description)
VALUES (1, 'Android Security Internals', '2014-10-14', 'Security book');
```

### READ (SELECT)

```sql
SELECT * FROM books;
```

### UPDATE

```sql
UPDATE books
SET name = 'New Book Name'
WHERE id = 1;
```

### DELETE

```sql
DELETE FROM books WHERE id = 1;
```

---

## ⚙️ SQL Clauses

Clauses are used to control and filter query results.

* **WHERE** – Filters records based on conditions
* **DISTINCT** – Returns unique values
* **ORDER BY** – Sorts results
* **GROUP BY** – Groups rows by a column
* **HAVING** – Filters grouped results

Example:

```sql
SELECT category, COUNT(*)
FROM hacking_tools
GROUP BY category
HAVING COUNT(*) > 1;
```

---

## 🔍 Operators

### Comparison Operators

* `=` Equal
* `!=` or `<>` Not equal
* `>`, `<`, `>=`, `<=`

### Logical Operators

* `AND`
* `OR`
* `NOT`

### Pattern Matching

```sql
SELECT * FROM books WHERE name LIKE '%security%';
```

---

## 🧮 SQL Functions

### Aggregate Functions

* `COUNT()` – Number of rows
* `SUM()` – Total value
* `MAX()` / `MIN()` – Maximum / Minimum value

Example:

```sql
SELECT COUNT(*) FROM hacking_tools;
```

### String Functions

* `LENGTH()` – String length
* `CONCAT()` – Combine strings

Example:

```sql
SELECT CONCAT(name, ' - ', category) FROM hacking_tools;
```

---

## 🧪 Practical Exercises (Examples)

Some example challenges solved during the room:

* Count distinct categories
* Find tools using specific filters
* Order results alphabetically
* Identify longest tool names
* Use aggregation functions to analyze data

---

## ✅ Key Takeaways

✔ Understanding of relational databases
✔ Hands-on experience with SQL queries
✔ Strong foundation for SQL Injection learning
✔ Useful knowledge for pentesting and defensive security

---

