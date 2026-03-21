# SQL Keys and Referential Integrity

## What are Keys?

Keys are columns (or groups of columns) used to **uniquely identify rows and create relationships between tables**.

Keys are fundamental to **relational database design** because they ensure:

* Rows are uniquely identifiable
* Relationships between tables remain consistent
* Invalid references cannot occur

---

# Primary Keys

A **PRIMARY KEY** uniquely identifies each row in a table.

Rules:

* Values must be **unique**
* Values cannot be **NULL**
* A table can have **only one primary key** (but it may contain multiple columns)

## Method 1: Inline Primary Key

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);
```

## Method 2: Table-Level Primary Key

```sql
CREATE TABLE employees (
    employee_id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    PRIMARY KEY (employee_id)
);
```

## Method 3: Composite Primary Key

A primary key composed of multiple columns.

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    semester VARCHAR(10),
    PRIMARY KEY (student_id, course_id)
);
```

---

# AUTO_INCREMENT

`AUTO_INCREMENT` automatically generates sequential values for a column, typically used for primary keys.

```sql
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);
```

Example inserts:

```sql
INSERT INTO employees (first_name, last_name)
VALUES ('Alice', 'Smith');

INSERT INTO employees (first_name, last_name)
VALUES ('Bob', 'Jones');
```

The database automatically assigns IDs such as `1`, `2`, `3`, etc.

---

# Foreign Keys

A **FOREIGN KEY** creates a relationship between two tables by referencing the primary key of another table.

* The referenced table is the **parent table**
* The referencing table is the **child table**

Example parent table:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);
```

Example child table:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

This ensures `department_id` in `employees` must exist in `departments`.

---

# Referential Integrity

**Referential integrity** ensures that relationships between tables remain valid.

For example:

* An employee cannot reference a department that does not exist
* A department cannot be removed if employees still reference it (depending on the rule applied)

These rules are controlled using **foreign key actions**.

---

# ON DELETE / ON UPDATE Actions

When a referenced row in the parent table changes or is removed, the database must decide what to do with related rows in the child table.

These actions are defined with `ON DELETE` and `ON UPDATE`.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```

---

# Foreign Key Action Types

## RESTRICT

Prevents the operation if related rows exist.

```sql
ON DELETE RESTRICT
```

If a department has employees, the department **cannot be deleted**.

---

## CASCADE

Automatically propagates the change to child rows.

```sql
ON DELETE CASCADE
```

If a department is deleted, **all employees in that department are also deleted**.

---

## SET NULL

Sets the foreign key column to `NULL` when the parent row is deleted.

```sql
ON DELETE SET NULL
```

Example result:

```
employee.department_id → NULL
```

---

## SET DEFAULT

Sets the foreign key column to its **default value**.

```sql
ON DELETE SET DEFAULT
```

This requires the column to have a `DEFAULT` value defined.

---

# Example with Multiple Rules

```sql
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);
```

Behavior:

* If a department ID changes → employee rows update automatically
* If a department is deleted → employee `department_id` becomes `NULL`

---

# Summary

| Concept                                     | Purpose                                     |
| ------------------------------------------- | ------------------------------------------- |
| PRIMARY KEY                                 | Uniquely identifies rows                    |
| AUTO_INCREMENT                              | Automatically generates IDs                 |
| FOREIGN KEY                                 | Links tables together                       |
| REFERENCES                                  | Specifies the parent table and column       |
| ON DELETE                                   | Defines behavior when parent row is deleted |
| ON UPDATE                                   | Defines behavior when parent key changes    |
| CASCADE / RESTRICT / SET NULL / SET DEFAULT | Control referential integrity actions       |

Keys and referential integrity ensure that **relationships between tables remain accurate and consistent** in relational databases.
