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

<div id="id-1"></div>

### 1) Basics

* NOT case-sensitive
* ends with ;
* Comments in SQL ```--comment``` or ```/* comment */```
>Ex: SELECT name, date, salary FROM employees WHERE salary > 25000;

***

<div id="id-2"></div>

### 2) Create database
> CREATE DATABASE database_name;

***

<div id="id-3"></div>

### 3) Create Table

```
CREATE TABLE table_name (
    column1_name data_type constraints,
    column2_name data_type constraints,
    ....
);
```

```
Example:

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

```
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

>INSERT INTO table_name (column1,column2,...) VALUES (value1,value2,...);
* Non-numeric values (strings, dates) must be surrounded by quotes

***

<div id="id-6"></div>

### 6) SELECT
* ```SELECT column1_name, column2_name, columnN_name FROM table_name;```
* ```SELECT * FROM table_name;```

***

<div id="id-7"></div>

### 7) WHERE
```
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

```
SELECT * FROM employees
WHERE salary > 1000 AND (dept_id = 2 OR dept_id = 4);
```

***

<div id="id-9"></div>

### 9) IN, BETWEEN

```
SELECT * FROM table_name
WHERE column_name IN (value1, value1,...);
```

```
SELECT column1_name, column2_name, columnN_name
FROM table_name
WHERE column_name BETWEEN min_value AND max_value;
```

* Date Range
```
SELECT * FROM employees WHERE hire_date
BETWEEN CAST('2006-01-01' AS DATE) AND CAST('2016-12-31' AS DATE);
```
* All names beginning with letter string range
```
SELECT * FROM employees
WHERE emp_name BETWEEN 'O' AND 'Z';
```

***