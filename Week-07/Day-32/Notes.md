# Python Full Stack Foundation

# Week-07 – Day-32

# MySQL Database

# CREATE TABLE, Data Types & Constraints

**Level:** Beginner → Intermediate

**Duration:** 2–3 Hours

---

# Learning Objectives

By the end of this session, you will be able to:

- Create Tables in MySQL
- Understand MySQL Data Types
- Use PRIMARY KEY
- Use AUTO_INCREMENT
- Apply Constraints
- Use DEFAULT Values
- Create Multiple Tables
- Describe Table Structure
- Modify Tables
- Delete Tables
- Understand Table Design Best Practices

---

# Agenda

1. CREATE TABLE
2. MySQL Data Types
3. Constraints
4. PRIMARY KEY
5. AUTO_INCREMENT
6. NOT NULL
7. UNIQUE
8. DEFAULT
9. CHECK
10. ALTER TABLE
11. DESCRIBE
12. SHOW CREATE TABLE

---

# Recap

Previous Session

✓ MySQL Installation

✓ Database Server

✓ MySQL Workbench

✓ CREATE DATABASE

✓ SHOW DATABASES

✓ USE Database

Today

We will create professional database tables.

---

# Database Structure

```
MySQL Server

↓

Database

↓

Tables

↓

Rows

↓

Columns
```

---

# What is a Table?

## Definition

A table is a collection of related data stored in rows and columns.

Example

```
Student

+----+--------+-------+

|ID  |Name    |Marks  |

+----+--------+-------+

|1   |Alex    |91     |

|2   |John    |85     |

+----+--------+-------+
```

---

# CREATE TABLE

## Definition

CREATE TABLE is a DDL command used to create a new table inside a database.

---

# Syntax

```sql
CREATE TABLE table_name(

column_name datatype,

column_name datatype

);
```

---

# Example

```sql
CREATE TABLE Student(

id INT,

name VARCHAR(100),

marks DECIMAL(5,2)

);
```

---

# Execute

```sql
USE college_db;

CREATE TABLE Student(

id INT,

name VARCHAR(100),

marks DECIMAL(5,2)

);
```

---

# Verify

```sql
SHOW TABLES;
```

Output

```
Student
```

---

# DESCRIBE TABLE

Displays table structure.

```sql
DESC Student;
```

or

```sql
DESCRIBE Student;
```

Output

```
Field

Type

Null

Key

Default

Extra
```

---

# SHOW CREATE TABLE

Displays complete SQL used to create a table.

```sql
SHOW CREATE TABLE Student;
```

Useful for

- Backup
- Documentation
- Debugging

---

# MySQL Data Types

```
Data Types

│

├── Numeric

├── String

├── Date & Time

└── Boolean
```

---

# Numeric Data Types

| Data Type | Description |
|------------|-------------|
| TINYINT | Very Small Integer |
| SMALLINT | Small Integer |
| INT | Integer |
| BIGINT | Large Integer |
| FLOAT | Approximate Decimal |
| DOUBLE | Large Decimal |
| DECIMAL | Exact Decimal |

---

# INT

Stores whole numbers.

```sql
age INT
```

Example

```
18

25

100

5000
```

---

# DECIMAL

Stores exact decimal values.

Best for

- Salary
- Price
- Bank Balance

Example

```sql
salary DECIMAL(10,2)
```

Possible Value

```
125000.50
```

---

# FLOAT

Stores approximate decimal values.

Suitable for

- Scientific calculations
- Measurements

Not recommended for financial values.

---

# String Data Types

| Type | Purpose |
|------|---------|
| CHAR | Fixed Length |
| VARCHAR | Variable Length |
| TEXT | Large Text |

---

# CHAR

Fixed length.

```sql
gender CHAR(1)
```

Example

```
M

F
```

---

# VARCHAR

Variable length.

```sql
name VARCHAR(100)
```

Example

```
Alex

Christopher

Ravi
```

Most commonly used string datatype.

---

# TEXT

Large amount of text.

Example

```sql
description TEXT
```

Suitable for

- Comments
- Reviews
- Articles
- Blog Content

---

# Date Data Types

| Type | Purpose |
|------|---------|
| DATE | Date |
| TIME | Time |
| DATETIME | Date & Time |
| TIMESTAMP | Automatic Time |

---

# DATE

```sql
dob DATE
```

Example

```
2001-05-18
```

---

# TIME

```sql
login_time TIME
```

Example

```
10:35:45
```

---

# DATETIME

```sql
created_at DATETIME
```

Example

```
2026-08-20 11:45:30
```

---

# BOOLEAN

Stored internally as

```
0

or

1
```

Example

```sql
is_active BOOLEAN
```

---

# PRIMARY KEY

## Definition

Uniquely identifies every row.

Example

```sql
student_id INT PRIMARY KEY
```

Rules

- Unique
- Cannot be NULL

---

# AUTO_INCREMENT

Automatically generates numbers.

Example

```sql
student_id INT AUTO_INCREMENT PRIMARY KEY
```

Output

```
1

2

3

4
```

---

# NOT NULL

Column cannot store NULL.

```sql
name VARCHAR(100)

NOT NULL
```

---

# UNIQUE

No duplicate values allowed.

```sql
email VARCHAR(100)

UNIQUE
```

---

# DEFAULT

Automatically assigns a value.

Example

```sql
status VARCHAR(20)

DEFAULT 'ACTIVE'
```

If no value is supplied,

```
ACTIVE
```

is inserted automatically.

---

# CHECK Constraint

Validates data.

```sql
marks DECIMAL(5,2)

CHECK(marks>=0 AND marks<=100)
```

---

# Complete Student Table

```sql
CREATE TABLE Student(

student_id INT AUTO_INCREMENT PRIMARY KEY,

name VARCHAR(100) NOT NULL,

email VARCHAR(100) UNIQUE,

department VARCHAR(50),

marks DECIMAL(5,2)

CHECK(marks>=0 AND marks<=100),

status VARCHAR(20)

DEFAULT 'ACTIVE'

);
```

---

# Employee Table

```sql
CREATE TABLE Employee(

emp_id INT AUTO_INCREMENT PRIMARY KEY,

name VARCHAR(100),

salary DECIMAL(10,2),

department VARCHAR(50),

joining_date DATE

);
```

---

# Product Table

```sql
CREATE TABLE Product(

product_id INT AUTO_INCREMENT PRIMARY KEY,

product_name VARCHAR(100),

price DECIMAL(10,2),

quantity INT,

category VARCHAR(50)

);
```

---

# Department Table

```sql
CREATE TABLE Department(

dept_id INT AUTO_INCREMENT PRIMARY KEY,

dept_name VARCHAR(100)

UNIQUE

);
```

---

# Book Table

```sql
CREATE TABLE Book(

book_id INT AUTO_INCREMENT PRIMARY KEY,

title VARCHAR(150),

author VARCHAR(100),

price DECIMAL(8,2)

);
```

---

# View All Tables

```sql
SHOW TABLES;
```

Output

```
Book

Department

Employee

Product

Student
```

---

# ALTER TABLE

## Definition

Used to modify an existing table.

---

# Add Column

```sql
ALTER TABLE Student

ADD phone VARCHAR(15);
```

---

# Add Multiple Columns

```sql
ALTER TABLE Student

ADD city VARCHAR(50),

ADD state VARCHAR(50);
```

---

# Modify Column

```sql
ALTER TABLE Student

MODIFY phone VARCHAR(20);
```

---

# Rename Column

```sql
ALTER TABLE Student

RENAME COLUMN phone

TO mobile;
```

(MySQL 8.0+)

---

# Drop Column

```sql
ALTER TABLE Student

DROP COLUMN mobile;
```

---

# Rename Table

```sql
RENAME TABLE Student

TO Students;
```

---

# Drop Table

Deletes the table permanently.

```sql
DROP TABLE Students;
```

---

# Truncate Table

Deletes all records.

Keeps table structure.

```sql
TRUNCATE TABLE Student;
```

---

# DROP vs TRUNCATE

| DROP | TRUNCATE |
|-------|----------|
| Deletes table | Deletes rows |
| Structure removed | Structure remains |
| Cannot insert immediately | Ready for new data |

---

# Complete Workflow

```
Create Database

↓

Use Database

↓

Create Table

↓

Describe Table

↓

Alter Table

↓

Insert Data
```

---

# Best Practices

✓ Use meaningful table names.

✓ Use PRIMARY KEY.

✓ Use AUTO_INCREMENT.

✓ Use NOT NULL where appropriate.

✓ Use DECIMAL for money values.

✓ Use VARCHAR instead of CHAR unless fixed length is required.

✓ Create constraints while creating the table.

---

# Common Mistakes

❌ Forgetting AUTO_INCREMENT.

❌ Using FLOAT for salaries.

❌ Not defining PRIMARY KEY.

❌ Creating duplicate email values without UNIQUE.

❌ Using TEXT for small strings.

---

# Practice Exercises

## Exercise 1

Create a Student table.

---

## Exercise 2

Create an Employee table.

---

## Exercise 3

Create a Product table.

---

## Exercise 4

Create a Library table.

---

## Exercise 5

Add a phone column to Student.

---

## Exercise 6

Rename phone to mobile.

---

## Exercise 7

Delete the mobile column.

---

## Exercise 8

Display table structure.

---

## Exercise 9

Display SQL used to create Student table.

---

## Exercise 10

Create a Customer table with

- customer_id
- name
- email
- city
- phone
- status

Use appropriate constraints.

---

# Interview Questions

### 1. What is the difference between CHAR and VARCHAR?

### 2. Why do we use AUTO_INCREMENT?

### 3. What is the purpose of PRIMARY KEY?

### 4. What is the difference between DROP and TRUNCATE?

### 5. Why is DECIMAL preferred over FLOAT for salary?

### 6. What does NOT NULL do?

### 7. What is the purpose of UNIQUE?

### 8. What is the difference between DESC and SHOW CREATE TABLE?

---

# Summary

Today we learned

✓ CREATE TABLE

✓ MySQL Data Types

✓ PRIMARY KEY

✓ AUTO_INCREMENT

✓ NOT NULL

✓ UNIQUE

✓ DEFAULT

✓ CHECK

✓ DESCRIBE

✓ SHOW CREATE TABLE

✓ ALTER TABLE

✓ DROP TABLE

✓ TRUNCATE TABLE

✓ Best Practices

---

# Coming Next (Day-33)

- INSERT Statement
- INSERT Multiple Records
- SELECT
- WHERE
- ORDER BY
- LIMIT
- UPDATE
- DELETE
- CRUD Operations in MySQL
- Importing Sample Data
- SQL Scripts
