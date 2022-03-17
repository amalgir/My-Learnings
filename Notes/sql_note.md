# SQL

## Contents

* [1) Basics](#id-1)
* [2) Create database](#id-2)
* [3) Create Table](#id-3)
* [4) SQL Constraints](#id-4)
* [5) INSERT](#id-5)
* [6) SELECT](#id-6)
* [7) WHERE](#id-7)
* [8) AND , OR](#id-8)
* [9) IN, BETWEEN](#id-9)
* [10) ORDERING](#id-10)
* [11) TOP / LIMIT](#id-11)
* [12) DISTINCT](#id-12)
* [13) UPDATE](#id-13)
* [14) DELETE](#id-14)
* [15) TRUNCATE TABLE](#id-15)
* [16) DROP TABLE](#id-16)

<div id="id-1"></div>

### 1) Basics

* NOT case-sensitive
* ends with ;
* Comments in SQL ```--comment``` or ```/* comment */```
```sql
SELECT name, date_of_join, salary FROM employees WHERE salary > 25000;
```

***

<div id="id-2"></div>

### 2) Create database
```sql
CREATE DATABASE database_name;
```

***

<div id="id-3"></div>

### 3) Create Table

```sql
CREATE TABLE table_name (
    column1_name data_type constraints,
    column2_name data_type constraints,
    ....
);
```

```sql
CREATE TABLE persons (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    birth_date DATE,
    phone VARCHAR(15) NOT NULL UNIQUE
);
```
* Data Types:
INT, DECIMAL, CHAR, VARCHAR, TEXT, DATE, DATETIME, TIMESTAMP
* Use ```CREATE TABLE IF NOT EXISTS``` to avoid error

***

<div id="id-4"></div>

### 4) SQL Constraints

| Constraint  | Description                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------|
| NOT NULL    | no null values in that column                                                                      |
| PRIMARY KEY | unique and not null                                                                                |
| UNIQUE      | unique, can have null values                                                                       |
| DEFAULT     | ```country VARCHAR(30) NOT NULL DEFAULT 'India'```                                                 |
| CHECK       | ```salary INT NOT NULL CHECK (salary >= 3000 AND salary <= 10000),```                              |
| FOREIGN KEY | connects primary key column of one table to the foreign key of another table ( same column values) |

```sql
CREATE TABLE employees (
    emp_id INT NOT NULL PRIMARY KEY,
    emp_name VARCHAR(55) NOT NULL,
    hire_date DATE NOT NULL,
    salary INT,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);
```
Here departments is another table with dept_id same as emp_id in employees table

***

<div id="id-5"></div>

### 5) INSERT

```sql
INSERT INTO table_name (column1,column2,...) VALUES (value1,value2,...);
```

* Non-numeric values (strings, dates) must be surrounded by quotes

***

<div id="id-6"></div>

### 6) SELECT
* ```SELECT column1_name, column2_name, columnN_name FROM table_name;```
* ```SELECT * FROM table_name;```

***

<div id="id-7"></div>

### 7) WHERE
```sql
SELECT * FROM employees
WHERE emp_id = 25;
```

WHERE Operators
* `=` `>` `<` `>=` `<=`
* LIKE `WHERE name LIKE 'Dav'`
* IN `WHERE country IN ('India', 'USA')`
* BETWEEN `WHERE age BETWEEN 33 AND 45`

***

<div id="id-8"></div>

### 8) AND , OR

```sql
SELECT * FROM employees
WHERE salary > 1000 AND (dept_id = 2 OR dept_id = 4);
```

***

<div id="id-9"></div>

### 9) IN, BETWEEN

```sql
SELECT * FROM table_name
WHERE column_name IN (value1, value1,...);
```

```sql
SELECT column1_name, column2_name, columnN_name
FROM table_name
WHERE column_name BETWEEN min_value AND max_value;
```

* Date Range
```sql
SELECT * FROM employees WHERE hire_date
BETWEEN CAST('2006-01-01' AS DATE) AND CAST('2016-12-31' AS DATE);
```
* All names beginning with letter string range
```sql
SELECT * FROM employees
WHERE emp_name BETWEEN 'O' AND 'Z';
```

***

<div id="id-10"></div>

### 10) ORDERING

```sql
SELECT column_list FROM table_name ORDER BY column_name ASC|DESC;
```
In case of string, it considers alphabetical order
```sql
SELECT * FROM employees 
ORDER BY salary DESC;
```

Sorting multiple column

```sql
SELECT * FROM employees 
ORDER BY first_name, last_name;
```
Here `last_name` is considered only if `first_name` has duplicates.

***

<div id="id-11"></div>

### 11) TOP / LIMIT

```sql
SELECT TOP number | percent column_list FROM table_name;
```

```sql
SELECT TOP 3 * FROM employees
ORDER BY salary DESC;
```

```sql
SELECT TOP 30 PERCENT * FROM employees
ORDER BY salary DESC;
```

#### MySQL syntax
```sql
SELECT column_list FROM table_name LIMIT number;
```

Also `LIMIT 2, 1`  means 2 is offset, 1 is no of rows

***

<div id="id-12"></div>

### 12) DISTINCT
Remove duplicates in the column - even nulls (only one null returned)
```sql
SELECT DISTINCT column_list FROM table_name;
```

```sql
SELECT DISTINCT country FROM customers;
```

***

<div id="id-13"></div>

### 13) UPDATE

```sql
UPDATE table_name
SET column1_name = value1, column2_name = value2,...
WHERE condition;
```

* Updating single column

```sql
UPDATE employees SET emp_name = 'Raj Kumar'
WHERE emp_id = 45;
```

* Updating multiple columns

```sql
UPDATE employees
SET salary = 9000, dept_id = 2
WHERE emp_id = 55;
```

***

<div id="id-14"></div>

### 14) DELETE

```sql
DELETE FROM table_name WHERE condition;
```

```sql
DELETE FROM employees WHERE id > 5;
```


#### Deletes all data from table
```sql
DELETE FROM employees;
```

***

<div id="id-15"></div>

### 15) TRUNCATE TABLE
* Deletes all rows
* Table structure remains
* faster than delete
```sql
TRUNCATE TABLE table_name;
```

***

<div id="id-16"></div>

### 16) DROP TABLE
* Permanently deletes table
```sql
DROP TABLE table1_name, table2_name, ...;
```
* Permanently deletes Database
```sql
DROP DATABASE demo;
```
***
