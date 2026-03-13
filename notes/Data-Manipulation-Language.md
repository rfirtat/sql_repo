# SQL Data Manipulation Language (DML)

## What is DML?

Data Manipulation Language (DML) is the subset of SQL used to **insert, modify, retrieve, and delete data** stored in database tables.

Unlike DDL, which defines database structure, DML works with the **actual records (rows)** inside tables.

Common DML operations include:

* Inserting new rows
* Updating existing rows
* Deleting rows
* Querying data

---

# INSERT

The `INSERT` statement adds new rows to a table.

## Insert a Row

```sql
INSERT INTO employees (employee_id, first_name, last_name, hire_date)
VALUES (1, 'Alice', 'Smith', '2024-01-15');
```

## Insert Without Specifying Columns

Columns must match the table order.

```sql
INSERT INTO employees
VALUES (2, 'Bob', 'Jones', '2024-03-01');
```

## Insert Multiple Rows

```sql
INSERT INTO employees (employee_id, first_name, last_name, hire_date)
VALUES
(3, 'Carol', 'Lee', '2024-04-10'),
(4, 'David', 'Nguyen', '2024-05-05');
```

---

# DEFAULT Values

Columns defined with `DEFAULT` automatically receive that value when no value is provided.

Table example:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    status VARCHAR(20) DEFAULT 'pending'
);
```

Insert using the default:

```sql
INSERT INTO orders (order_id)
VALUES (101);
```

Explicitly using `DEFAULT`:

```sql
INSERT INTO orders (order_id, status)
VALUES (102, DEFAULT);
```

---

# UPDATE

The `UPDATE` statement modifies existing rows.

## Basic Update

```sql
UPDATE employees
SET last_name = 'Johnson'
WHERE employee_id = 2;
```

## Update Multiple Columns

```sql
UPDATE employees
SET first_name = 'Robert',
    hire_date = '2024-02-01'
WHERE employee_id = 2;
```

⚠️ If `WHERE` is omitted, **all rows will be updated**.

---

# DELETE

The `DELETE` statement removes rows from a table.

## Delete Specific Rows

```sql
DELETE FROM employees
WHERE employee_id = 4;
```

## Delete Multiple Rows

```sql
DELETE FROM employees
WHERE hire_date < '2024-01-01';
```

## Delete All Rows

```sql
DELETE FROM employees;
```

This removes all rows but **keeps the table structure**.

---

# SELECT (Querying Data)

Although sometimes categorized separately, `SELECT` is often grouped with DML because it retrieves data.

```sql
SELECT first_name, last_name
FROM employees
WHERE hire_date > '2024-01-01';
```

---

# Summary

DML commands manipulate the **data inside tables**.

| Command | Purpose              |
| ------- | -------------------- |
| INSERT  | Add new rows         |
| UPDATE  | Modify existing rows |
| DELETE  | Remove rows          |
| SELECT  | Retrieve data        |

DML focuses on **working with records**, while DDL focuses on **database structure**.
