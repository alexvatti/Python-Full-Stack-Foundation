# Python Full Stack Foundation

# Week-07 – Day-33

# MySQL Database

# CRUD Operations (INSERT, SELECT, UPDATE & DELETE)

**Level:** Beginner → Intermediate

**Duration:** 2–3 Hours

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand CRUD Operations
- Insert Records into MySQL Tables
- Insert Multiple Records
- Retrieve Records using SELECT
- Filter Data using WHERE
- Sort Data using ORDER BY
- Limit Results using LIMIT
- Update Existing Records
- Delete Records
- Use Parameterized Queries (Python)
- Understand SQL Injection
- Perform Complete CRUD Operations

---

# Agenda

1. CRUD Operations
2. INSERT
3. INSERT Multiple Rows
4. SELECT
5. WHERE
6. ORDER BY
7. LIMIT
8. UPDATE
9. DELETE
10. SQL Injection
11. Parameterized Queries
12. Python + MySQL

---

# Recap

Previous Session

✓ CREATE TABLE

✓ PRIMARY KEY

✓ AUTO_INCREMENT

✓ Constraints

✓ ALTER TABLE

✓ DESCRIBE

Today

We will start working with data inside tables.

---

# What is CRUD?

CRUD stands for

```
Create

Read

Update

Delete
```

Every database application performs these four operations.

---

# CRUD Workflow

```
Application

↓

INSERT

↓

SELECT

↓

UPDATE

↓

DELETE

↓

Database
```

---

# Sample Student Table

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|
|2|John|ECE|84|
|3|Priya|IT|95|

---

# INSERT Statement

## Definition

INSERT is used to add new records into a table.

---

# Syntax

```sql
INSERT INTO table_name

(column1,column2,column3)

VALUES

(value1,value2,value3);
```

---

# Example

```sql
INSERT INTO Student

(name,department,marks)

VALUES

('Alex','CSE',91);
```

---

# Why ID is Not Given?

Because

```
AUTO_INCREMENT
```

automatically generates IDs.

Example

```
1

2

3

4

5
```

---

# Insert Second Record

```sql
INSERT INTO Student

(name,department,marks)

VALUES

('John','ECE',84);
```

---

# Insert Third Record

```sql
INSERT INTO Student

(name,department,marks)

VALUES

('Priya','IT',95);
```

---

# View Data

```sql
SELECT *

FROM Student;
```

Output

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|
|2|John|ECE|84|
|3|Priya|IT|95|

---

# Insert Multiple Rows

```sql
INSERT INTO Student

(name,department,marks)

VALUES

('Ravi','EEE',82),

('Neha','CSE',89),

('David','IT',78);
```

One statement inserts multiple rows.

---

# INSERT Using SET

```sql
INSERT INTO Student

SET

name='Kiran',

department='MBA',

marks=87;
```

MySQL supports this syntax.

---

# SELECT Statement

## Definition

SELECT retrieves records from a table.

---

# Syntax

```sql
SELECT *

FROM Student;
```

---

# Select Specific Columns

```sql
SELECT

name,

marks

FROM Student;
```

Output

```
Alex      91

John      84

Priya     95
```

---

# Display Department Only

```sql
SELECT department

FROM Student;
```

Duplicates may appear.

---

# DISTINCT

Remove duplicate values.

```sql
SELECT DISTINCT

department

FROM Student;
```

Output

```
CSE

ECE

IT

EEE

MBA
```

---

# WHERE Clause

## Definition

WHERE filters records.

---

# Example

```sql
SELECT *

FROM Student

WHERE department='CSE';
```

---

# Numeric Example

Students scoring above 90.

```sql
SELECT *

FROM Student

WHERE marks>90;
```

---

# Multiple Conditions

```sql
SELECT *

FROM Student

WHERE

department='IT'

AND

marks>80;
```

---

# OR Condition

```sql
SELECT *

FROM Student

WHERE

department='CSE'

OR

department='ECE';
```

---

# Comparison Operators

| Operator | Meaning |
|-----------|---------|
| = | Equal |
| > | Greater Than |
| < | Less Than |
| >= | Greater Than or Equal |
| <= | Less Than or Equal |
| <> | Not Equal |

---

# ORDER BY

Sorts records.

---

# Ascending

```sql
SELECT *

FROM Student

ORDER BY marks;
```

---

# Descending

```sql
SELECT *

FROM Student

ORDER BY marks DESC;
```

---

# Sort by Name

```sql
SELECT *

FROM Student

ORDER BY name;
```

---

# Sort by Department then Marks

```sql
SELECT *

FROM Student

ORDER BY

department,

marks DESC;
```

---

# LIMIT

Returns only required records.

---

# Example

```sql
SELECT *

FROM Student

LIMIT 5;
```

---

# Second Example

Top 3 Students

```sql
SELECT *

FROM Student

ORDER BY marks DESC

LIMIT 3;
```

---

# OFFSET

Skip records.

```sql
SELECT *

FROM Student

LIMIT 5 OFFSET 5;
```

Displays

Records 6–10.

---

# UPDATE Statement

## Definition

UPDATE modifies existing records.

---

# Syntax

```sql
UPDATE Student

SET marks=95

WHERE student_id=1;
```

---

# Example

Before

```
Alex

91
```

After

```
Alex

95
```

---

# Update Multiple Columns

```sql
UPDATE Student

SET

department='AI',

marks=98

WHERE student_id=2;
```

---

# UPDATE with Condition

```sql
UPDATE Student

SET marks=100

WHERE department='CSE';
```

Only CSE students are updated.

---

# DELETE Statement

## Definition

DELETE removes records.

---

# Syntax

```sql
DELETE

FROM Student

WHERE student_id=3;
```

---

# Delete All Records

```sql
DELETE

FROM Student;
```

Table remains.

Only data is deleted.

---

# DROP TABLE

```sql
DROP TABLE Student;
```

Deletes

- Table
- Data
- Structure

Everything is removed.

---

# DELETE vs TRUNCATE vs DROP

| DELETE | TRUNCATE | DROP |
|---------|-----------|------|
| Removes Rows | Removes All Rows | Removes Table |
| WHERE Allowed | WHERE Not Allowed | Table Deleted |
| Structure Exists | Structure Exists | Structure Removed |

---

# LIKE Operator

Searches patterns.

---

Starts with A

```sql
SELECT *

FROM Student

WHERE name LIKE 'A%';
```

---

Ends with a

```sql
SELECT *

FROM Student

WHERE name LIKE '%a';
```

---

Contains "ri"

```sql
SELECT *

FROM Student

WHERE name LIKE '%ri%';
```

---

# BETWEEN

```sql
SELECT *

FROM Student

WHERE marks

BETWEEN 80 AND 90;
```

---

# IN Operator

```sql
SELECT *

FROM Student

WHERE department

IN ('CSE','IT');
```

---

# NULL Values

Find students without email.

```sql
SELECT *

FROM Student

WHERE email IS NULL;
```

---

# Aliases

```sql
SELECT

name AS StudentName,

marks AS Score

FROM Student;
```

Output

```
StudentName

Score
```

---

# Complete Report

```sql
SELECT

student_id,

name,

department,

marks

FROM Student

ORDER BY marks DESC;
```

---

# SQL Injection

Suppose user enters

```
' OR 1=1 --
```

If SQL is created using string concatenation,

all records may be displayed.

---

# Incorrect Python Code

```python
sql = "SELECT * FROM Student WHERE name='" + name + "'"
```

Unsafe.

---

# Correct Python Code

```python
cursor.execute(

"SELECT * FROM Student WHERE name=%s",

(name,)

)
```

Safe.

---

# Why Parameterized Queries?

Benefits

✓ Prevent SQL Injection

✓ Cleaner Code

✓ Better Performance

✓ Easier Maintenance

---

# Python MySQL Connector

Install

```bash
pip install mysql-connector-python
```

---

# Connect MySQL

```python
import mysql.connector

connection = mysql.connector.connect(

host="localhost",

user="root",

password="root123",

database="college_db"

)

print("Connected")
```

---

# Create Cursor

```python
cursor = connection.cursor()
```

---

# INSERT Using Python

```python
sql="""

INSERT INTO Student

(name,department,marks)

VALUES(%s,%s,%s)

"""

values=("Alex","CSE",91)

cursor.execute(sql,values)

connection.commit()
```

---

# SELECT Using Python

```python
cursor.execute(

"SELECT * FROM Student"

)

rows=cursor.fetchall()

for row in rows:

    print(row)
```

---

# UPDATE Using Python

```python
sql="""

UPDATE Student

SET marks=%s

WHERE student_id=%s

"""

cursor.execute(sql,(95,1))

connection.commit()
```

---

# DELETE Using Python

```python
sql="""

DELETE FROM Student

WHERE student_id=%s

"""

cursor.execute(sql,(3,))

connection.commit()
```

---

# Complete CRUD Flow

```
Python

↓

MySQL Connector

↓

MySQL Server

↓

Student Table

↓

CRUD Operations
```

---

# Best Practices

✓ Always use WHERE with UPDATE.

✓ Always use WHERE with DELETE.

✓ Use parameterized queries.

✓ Commit changes after INSERT, UPDATE and DELETE.

✓ Close database connections.

✓ Use meaningful table names.

---

# Common Mistakes

❌ Forgetting WHERE.

Example

```sql
UPDATE Student

SET marks=100;
```

Every student becomes

```
100
```

---

❌ Deleting all rows accidentally.

```sql
DELETE FROM Student;
```

---

❌ Forgetting

```sql
COMMIT;
```

(Required when auto-commit is disabled.)

---

❌ Using string concatenation in Python.

Always use

```python
%s
```

placeholders.

---

# Practice Exercises

## Exercise 1

Insert 10 students.

---

## Exercise 2

Display all students.

---

## Exercise 3

Display students from CSE.

---

## Exercise 4

Display students scoring above 85.

---

## Exercise 5

Sort students by marks.

---

## Exercise 6

Display top 5 students.

---

## Exercise 7

Update one student's marks.

---

## Exercise 8

Delete one student.

---

## Exercise 9

Display unique departments.

---

## Exercise 10

Write a Python program that

- Connects to MySQL
- Inserts one student
- Displays all students
- Updates marks
- Deletes one student
- Displays final records

---

# Interview Questions

### 1. What is CRUD?

### 2. What is the difference between DELETE and DROP?

### 3. Why do we use WHERE with UPDATE?

### 4. What is SQL Injection?

### 5. Why are parameterized queries recommended?

### 6. What is the difference between LIMIT and OFFSET?

### 7. What does DISTINCT do?

### 8. What is the purpose of ORDER BY?

---

# Summary

Today we learned

✓ CRUD Operations

✓ INSERT

✓ INSERT Multiple Rows

✓ SELECT

✓ DISTINCT

✓ WHERE

✓ ORDER BY

✓ LIMIT

✓ OFFSET

✓ UPDATE

✓ DELETE

✓ LIKE

✓ BETWEEN

✓ IN

✓ Parameterized Queries

✓ SQL Injection

✓ Python MySQL Connector

✓ CRUD using Python

---

# Coming Next (Day-34)

- Aggregate Functions
- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()
- GROUP BY
- HAVING
- MySQL Built-in Functions
- Date Functions
- String Functions
- Numeric Functions
- Real-world SQL Reports
