# SQL Constraints

## What are Constraints?

Constraints are rules applied to table columns that **control what data can be inserted or stored** in a database.

They help maintain:

* Data accuracy
* Data consistency
* Data integrity

Constraints can be defined **when a table is created** or **added later using `ALTER TABLE`**.

---

# Column vs Table Constraints

Constraints can be defined in two ways.

## Column Constraints

Defined **directly next to a column definition**.

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    age INT CHECK (age >= 18)
);
```

These constraints apply **only to that column**.

---

## Table Constraints

Defined **separately at the end of the table definition**.

```sql
CREATE TABLE users (
    user_id INT,
    email VARCHAR(100),
    age INT,
    CONSTRAINT pk_users PRIMARY KEY (user_id),
    CONSTRAINT uq_email UNIQUE (email),
    CONSTRAINT chk_age CHECK (age >= 18)
);
```

Table constraints are often used when:

* Naming constraints
* Applying constraints to **multiple columns**

---

# Common Constraints

## NOT NULL

Ensures a column **cannot contain NULL values**.

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

---

## UNIQUE

Ensures all values in a column (or group of columns) are **distinct**.

### Column Example

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

### Table Example

```sql
CREATE TABLE users (
    user_id INT,
    email VARCHAR(100),
    CONSTRAINT uq_email UNIQUE (email)
);
```

Composite unique constraint:

```sql
CONSTRAINT uq_user UNIQUE (first_name, last_name)
```

---

## CHECK

Ensures values satisfy a **logical condition**.

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    price DECIMAL(10,2) CHECK (price > 0)
);
```

Multiple rules example:

```sql
CHECK (age >= 18 AND age <= 120)
```

---

## DEFAULT

Provides a **default value** if none is supplied.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    status VARCHAR(20) DEFAULT 'pending'
);
```

Example insert:

```sql
INSERT INTO orders (order_id)
VALUES (101);
```

Result:

```
status = 'pending'
```

---

## PRIMARY KEY

A special constraint that:

* Uniquely identifies rows
* Cannot contain NULL values

```sql
PRIMARY KEY (id)
```

---

## FOREIGN KEY

Links a column to a primary key in another table.

```sql
FOREIGN KEY (department_id)
REFERENCES departments(department_id)
```

This enforces **referential integrity**.

---

# Adding Constraints

Constraints can be added after table creation.

```sql
ALTER TABLE users
ADD CONSTRAINT uq_email UNIQUE (email);
```

Add a check constraint:

```sql
ALTER TABLE products
ADD CONSTRAINT chk_price CHECK (price > 0);
```

---

# Dropping Constraints

Constraints can also be removed.

```sql
ALTER TABLE users
DROP CONSTRAINT uq_email;
```

Dropping a foreign key example:

```sql
ALTER TABLE employees
DROP CONSTRAINT fk_department;
```

(Some databases require `DROP INDEX` or slightly different syntax.)

---

# Naming Constraints

Constraints can be explicitly named using `CONSTRAINT`.

```sql
CONSTRAINT chk_age CHECK (age >= 18)
```

Benefits of naming constraints:

* Easier to modify or remove later
* More readable schema

---

# Summary

| Constraint  | Purpose                                |
| ----------- | -------------------------------------- |
| NOT NULL    | Prevents NULL values                   |
| UNIQUE      | Ensures values are distinct            |
| CHECK       | Enforces logical conditions            |
| DEFAULT     | Provides automatic value               |
| PRIMARY KEY | Unique row identifier                  |
| FOREIGN KEY | Maintains relationships between tables |

Constraints help ensure **data quality and integrity** in relational databases.
