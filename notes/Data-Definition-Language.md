# SQL Data Definition Language (DDL)

## What is DDL?

Data Definition Language (DDL) is the subset of SQL used to **define, modify, and remove database structures**. These structures include databases, tables, and constraints.

Common DDL operations include:

* Creating databases and tables
* Modifying table structure
* Deleting databases or tables
* Defining constraints that enforce data rules

---

# Databases

## Create Database

Creates a new database.

```sql
CREATE DATABASE company_db;
```

## Show Databases

Lists all databases on the server.

```sql
SHOW DATABASES;
```

## Select Database

Selects a database to work with.

```sql
USE company_db;
```

## Drop Database

Deletes a database and all of its contents.

```sql
DROP DATABASE company_db;
```

---

# Tables

## Create Table

Defines a new table and its columns.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    hire_date DATE
);
```

## Show Tables

Lists all tables in the current database.

```sql
SHOW TABLES;
```

## Show Table Structure

Displays the schema of a table.

```sql
SHOW CREATE TABLE employees;
```

or

```sql
DESCRIBE employees;
```

## Drop Table

Deletes a table and its data.

```sql
DROP TABLE employees;
```

---

# ALTER TABLE

`ALTER TABLE` modifies the structure of an existing table.

## Add Column

```sql
ALTER TABLE employees
ADD salary DECIMAL(10,2);
```

## Modify / Change Column

```sql
ALTER TABLE employees
MODIFY salary DECIMAL(12,2);
```

Rename a column:

```sql
ALTER TABLE employees
CHANGE salary annual_salary DECIMAL(12,2);
```

## Drop Column

```sql
ALTER TABLE employees
DROP COLUMN annual_salary;
```

---

# Constraints

Constraints enforce rules on the data stored in tables.

Common constraints:

| Constraint  | Description                                      |
| ----------- | ------------------------------------------------ |
| PRIMARY KEY | Uniquely identifies each row in a table          |
| FOREIGN KEY | Links a column to a primary key in another table |
| UNIQUE      | Ensures all values in a column are different     |
| NOT NULL    | Prevents NULL values                             |
| CHECK       | Ensures values meet a condition                  |
| DEFAULT     | Assigns a default value                          |

Example:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,
    amount DECIMAL(10,2) CHECK (amount > 0),
    order_date DATE DEFAULT CURRENT_DATE
);
```

## Adding a Constraint

```sql
ALTER TABLE orders
ADD CONSTRAINT fk_customer
FOREIGN KEY (customer_id)
REFERENCES customers(customer_id);
```

## Dropping a Constraint

```sql
ALTER TABLE orders
DROP CONSTRAINT fk_customer;
```

---

# Summary

DDL commands define and control database structure.

Common commands:

| Command | Purpose                     |
| ------- | --------------------------- |
| CREATE  | Create databases or tables  |
| SHOW    | Display databases or tables |
| USE     | Select a database           |
| ALTER   | Modify table structure      |
| DROP    | Delete databases or tables  |

DDL focuses on **schema design**, not manipulating the data itself (which is handled by DML).
