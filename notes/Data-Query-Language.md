# SQL Data Query Language (DQL)

## What is DQL?

Data Query Language (DQL) is the subset of SQL used to **retrieve data from a database**. The primary command in DQL is `SELECT`, which allows users to query tables and return specific rows and columns.

DQL focuses on **reading data**, not modifying it.

Common query tasks include:

* Selecting specific columns
* Filtering rows
* Limiting results
* Sorting results

---

# SELECT and FROM

The `SELECT` clause specifies the columns to retrieve, and the `FROM` clause specifies the table.

## Select Specific Columns

```sql
SELECT first_name, last_name
FROM employees;
```

## Select All Columns

```sql
SELECT *
FROM employees;
```

---

# WHERE

The `WHERE` clause filters rows based on a condition.

```sql
SELECT first_name, last_name
FROM employees
WHERE hire_date > '2024-01-01';
```

## Multiple Conditions

```sql
SELECT *
FROM employees
WHERE department = 'Sales'
AND hire_date > '2023-01-01';
```

Common operators:

| Operator     | Meaning                             |
| ------------ | ----------------------------------- |
| =            | Equal                               |
| != or <>     | Not equal                           |
| >, <, >=, <= | Comparison                          |
| AND          | Both conditions must be true        |
| OR           | At least one condition must be true |
| NOT          | Negates a condition                 |

---

# LIMIT

The `LIMIT` clause restricts the number of rows returned.

```sql
SELECT *
FROM employees
LIMIT 5;
```

This returns only the first 5 rows from the result set.

---

# ORDER BY

Sorts the results.

```sql
SELECT first_name, hire_date
FROM employees
ORDER BY hire_date DESC;
```

* `ASC` → ascending (default)
* `DESC` → descending

---

# DISTINCT

Removes duplicate results.

```sql
SELECT DISTINCT department
FROM employees;
```

---

# Basic Query Structure

A common query structure looks like:

```sql
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column
LIMIT number;
```

---

# Summary

DQL commands retrieve data from the database.

| Clause   | Purpose                   |
| -------- | ------------------------- |
| SELECT   | Choose columns to display |
| FROM     | Specify the table         |
| WHERE    | Filter rows               |
| ORDER BY | Sort results              |
| LIMIT    | Restrict number of rows   |
| DISTINCT | Remove duplicate values   |

DQL is focused on **querying and exploring data without changing it**.
