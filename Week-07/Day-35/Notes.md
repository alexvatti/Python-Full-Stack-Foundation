# Python Full Stack Foundation

# Week-07 – Day-35

# MySQL Database

# Table Relationships, Joins & Database Design

**Level:** Beginner → Intermediate

**Duration:** 3 Hours

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Database Relationships
- Create Primary Keys and Foreign Keys
- Understand Referential Integrity
- Perform INNER JOIN
- Perform LEFT JOIN
- Perform RIGHT JOIN
- Perform CROSS JOIN
- Perform SELF JOIN
- Understand Database Normalization
- Design a Complete College Database
- Write Multi-table SQL Queries

---

# Agenda

1. Database Relationships
2. Primary Key
3. Foreign Key
4. Referential Integrity
5. One-to-One Relationship
6. One-to-Many Relationship
7. Many-to-Many Relationship
8. INNER JOIN
9. LEFT JOIN
10. RIGHT JOIN
11. CROSS JOIN
12. SELF JOIN
13. Normalization
14. College Database Design

---

# Recap

Previous Session

✓ Aggregate Functions

✓ GROUP BY

✓ HAVING

✓ MySQL Functions

✓ Reports

Today

We will connect multiple tables together.

---

# Why Multiple Tables?

Imagine storing student data like this.

| Student | Department | HOD | Course |
|----------|------------|------|--------|
|Alex|CSE|Ravi|Python|
|Alex|CSE|Ravi|SQL|
|Alex|CSE|Ravi|Java|

Notice

- Student repeats
- Department repeats
- HOD repeats

This creates

❌ Duplicate Data

❌ Wasted Storage

❌ Difficult Updates

---

# Better Database Design

```
Department

↓

Student

↓

Enrollment

↓

Course
```

Each table stores only one type of information.

---

# What is a Relationship?

## Definition

A relationship is a connection between two database tables using a **Primary Key** and a **Foreign Key**.

---

# Primary Key

## Definition

A Primary Key uniquely identifies each record.

Example

```
Student

ID

1

2

3

4
```

Rules

✓ Unique

✓ Cannot be NULL

✓ One Primary Key per table

---

# Foreign Key

## Definition

A Foreign Key references the Primary Key of another table.

It establishes relationships.

---

# Example

Department Table

| Dept_ID | Department |
|---------|------------|
|1|CSE|
|2|ECE|
|3|IT|

Student Table

| Student | Dept_ID |
|----------|---------|
|Alex|1|
|John|2|
|Mary|3|

Dept_ID connects both tables.

---

# Creating Department Table

```sql
CREATE TABLE Department(

dept_id INT AUTO_INCREMENT PRIMARY KEY,

dept_name VARCHAR(50)

);
```

---

# Creating Student Table

```sql
CREATE TABLE Student(

student_id INT AUTO_INCREMENT PRIMARY KEY,

student_name VARCHAR(100),

dept_id INT,

FOREIGN KEY(dept_id)

REFERENCES Department(dept_id)

);
```

---

# Referential Integrity

## Definition

Referential Integrity ensures that every Foreign Key value must exist in the referenced table.

Example

Department

```
1

2

3
```

Student

```
Dept_ID = 5
```

❌ Invalid

Because Department 5 does not exist.

---

# Types of Relationships

```
Relationships

│

├── One-to-One

├── One-to-Many

└── Many-to-Many
```

---

# One-to-One Relationship

One student

↓

One ID Card

```
Student

↓

ID Card
```

---

# Example

Student

| ID | Name |
|----|------|
|1|Alex|

IDCard

| Card_ID | Student_ID |
|----------|------------|
|101|1|

---

# SQL

```sql
CREATE TABLE IDCard(

card_id INT PRIMARY KEY,

student_id INT UNIQUE,

FOREIGN KEY(student_id)

REFERENCES Student(student_id)

);
```

---

# One-to-Many Relationship

Most common relationship.

Department

↓

Many Students

```
Department

↓

Student

Student

Student
```

---

Example

| Department | Students |
|------------|----------|
|CSE|Alex|
|CSE|Priya|
|CSE|Ravi|

---

# Many-to-Many Relationship

Students

↓

Many Courses

Courses

↓

Many Students

---

Solution

Use a Junction Table.

```
Student

↓

Enrollment

↓

Course
```

---

# Enrollment Table

```sql
CREATE TABLE Enrollment(

student_id INT,

course_id INT,

PRIMARY KEY(student_id,course_id),

FOREIGN KEY(student_id)

REFERENCES Student(student_id),

FOREIGN KEY(course_id)

REFERENCES Course(course_id)

);
```

---

# Sample Tables

Department

| Dept_ID | Department |
|---------|------------|
|1|CSE|
|2|ECE|
|3|IT|

---

Student

| Student_ID | Name | Dept_ID |
|-----------|------|---------|
|1|Alex|1|
|2|John|2|
|3|Mary|3|

---

# What is JOIN?

## Definition

JOIN combines rows from two or more tables using a related column.

Without JOIN

Tables remain separate.

With JOIN

Information is combined.

---

# Types of JOIN

```
JOIN

│

├── INNER JOIN

├── LEFT JOIN

├── RIGHT JOIN

├── CROSS JOIN

└── SELF JOIN
```

---

# INNER JOIN

Returns only matching records.

---

Example

```sql
SELECT

Student.student_name,

Department.dept_name

FROM Student

INNER JOIN Department

ON Student.dept_id=Department.dept_id;
```

---

Output

| Student | Department |
|----------|------------|
|Alex|CSE|
|John|ECE|
|Mary|IT|

---

# INNER JOIN Diagram

```
Student

●●●●

Department

●●●●

Only Matching Records
```

---

# LEFT JOIN

Returns

All rows from Left Table

+

Matching rows from Right Table

---

Example

```sql
SELECT

Student.student_name,

Department.dept_name

FROM Student

LEFT JOIN Department

ON Student.dept_id=Department.dept_id;
```

Even if Department is NULL,

student will appear.

---

# LEFT JOIN Diagram

```
Student

★★★★★

Department

★★★

Result

★★★★★
```

---

# RIGHT JOIN

Returns

All rows from Right Table

+

Matching rows from Left Table

---

Example

```sql
SELECT

Student.student_name,

Department.dept_name

FROM Student

RIGHT JOIN Department

ON Student.dept_id=Department.dept_id;
```

---

# RIGHT JOIN Diagram

```
Department

★★★★★

Student

★★★

Result

★★★★★
```

---

# CROSS JOIN

Returns

Every combination.

Formula

```
RowsA × RowsB
```

Example

3 Students

×

2 Departments

=

6 Rows

---

SQL

```sql
SELECT *

FROM Student

CROSS JOIN Department;
```

---

# CROSS JOIN Result

| Student | Department |
|----------|------------|
|Alex|CSE|
|Alex|ECE|
|John|CSE|
|John|ECE|
|Mary|CSE|
|Mary|ECE|

---

# SELF JOIN

A table joins with itself.

Useful when

Employee

↓

Manager

are stored in same table.

---

Employee Table

| ID | Name | Manager_ID |
|----|------|-----------|
|1|John|NULL|
|2|Alex|1|
|3|David|1|

---

SQL

```sql
SELECT

e.name Employee,

m.name Manager

FROM Employee e

LEFT JOIN Employee m

ON e.manager_id=m.id;
```

---

Output

| Employee | Manager |
|-----------|----------|
|Alex|John|
|David|John|

---

# Multiple JOIN Example

```sql
SELECT

Student.student_name,

Department.dept_name,

Course.course_name

FROM Student

INNER JOIN Department

ON Student.dept_id=Department.dept_id

INNER JOIN Enrollment

ON Student.student_id=Enrollment.student_id

INNER JOIN Course

ON Enrollment.course_id=Course.course_id;
```

---

# College Database

```
Department

↓

Teacher

↓

Course

↓

Enrollment

↓

Student
```

---

# Complete ER Diagram

```
Department

│

├── Teacher

│

├── Student

│

└── Course

        │

        └── Enrollment
```

---

# Normalization

## Definition

Normalization is the process of organizing data to eliminate redundancy and improve data integrity.

---

# Why Normalize?

Benefits

✓ Less Duplicate Data

✓ Easier Updates

✓ Better Performance

✓ Better Data Integrity

---

# First Normal Form (1NF)

Rules

- Atomic values
- No repeating columns

Bad

| Student | Subjects |
|----------|----------|
|Alex|Python,SQL|

Good

| Student | Subject |
|----------|---------|
|Alex|Python|
|Alex|SQL|

---

# Second Normal Form (2NF)

Rules

- Must satisfy 1NF
- Remove partial dependency

Store student information separately from course information.

---

# Third Normal Form (3NF)

Rules

- Must satisfy 2NF
- Remove transitive dependency

Department name should not be repeated in Student table.

---

# Real World Example

Hospital

```
Patient

↓

Doctor

↓

Appointment
```

---

# Banking Example

```
Customer

↓

Account

↓

Transactions
```

---

# E-Commerce Example

```
Customer

↓

Orders

↓

Products

↓

Order_Items
```

---

# Python Example

```python
import mysql.connector

connection = mysql.connector.connect(

host="localhost",

user="root",

password="root123",

database="college_db"

)

cursor=connection.cursor()

query="""

SELECT

Student.student_name,

Department.dept_name

FROM Student

INNER JOIN Department

ON Student.dept_id=Department.dept_id

"""

cursor.execute(query)

rows=cursor.fetchall()

for row in rows:

    print(row)

connection.close()
```

---

# JOIN Summary

| JOIN | Returns |
|------|----------|
| INNER JOIN | Matching rows |
| LEFT JOIN | All Left + Matching Right |
| RIGHT JOIN | All Right + Matching Left |
| CROSS JOIN | Every Combination |
| SELF JOIN | Same Table Joined |

---

# Best Practices

✓ Always use Primary Keys.

✓ Use Foreign Keys.

✓ Avoid duplicate information.

✓ Use aliases for readability.

✓ Use meaningful table names.

✓ Normalize the database.

---

# Common Mistakes

❌ Storing department name repeatedly.

❌ No Primary Key.

❌ No Foreign Key.

❌ Forgetting ON condition.

Bad

```sql
SELECT *

FROM Student

JOIN Department;
```

Correct

```sql
SELECT *

FROM Student

JOIN Department

ON Student.dept_id=Department.dept_id;
```

---

# Practice Exercises

## Exercise 1

Create Department and Student tables.

---

## Exercise 2

Create Course table.

---

## Exercise 3

Create Enrollment table.

---

## Exercise 4

Insert sample data.

---

## Exercise 5

Display Student Name with Department.

---

## Exercise 6

Display Student Name with Course Name.

---

## Exercise 7

Display Department-wise Student Count.

---

## Exercise 8

Find students who are not enrolled in any course.

---

## Exercise 9

Create Employee table with Manager relationship.

---

## Exercise 10

Design a Hospital database with

- Patient
- Doctor
- Appointment
- Medicine
- Billing

---

# Interview Questions

### 1. What is the difference between Primary Key and Foreign Key?

### 2. What is Referential Integrity?

### 3. Explain One-to-One Relationship.

### 4. Explain One-to-Many Relationship.

### 5. Explain Many-to-Many Relationship.

### 6. What is a Junction Table?

### 7. Difference between INNER JOIN and LEFT JOIN?

### 8. What is CROSS JOIN?

### 9. What is SELF JOIN?

### 10. What is Database Normalization?

### 11. Explain 1NF, 2NF and 3NF.

### 12. Why are Foreign Keys important?

---

# Summary

Today we learned

✓ Database Relationships

✓ Primary Key

✓ Foreign Key

✓ Referential Integrity

✓ One-to-One Relationship

✓ One-to-Many Relationship

✓ Many-to-Many Relationship

✓ INNER JOIN

✓ LEFT JOIN

✓ RIGHT JOIN

✓ CROSS JOIN

✓ SELF JOIN

✓ Normalization (1NF, 2NF, 3NF)

✓ Multi-table Queries

✓ College Database Design

---

# Week-08 Preview

From the next session, we move beyond SQL fundamentals into **Python + MySQL Integration**, where you will learn to build complete database applications.

Topics include:

- Installing `mysql-connector-python`
- Connecting Python to MySQL
- Executing SQL from Python
- CRUD Operations using Python
- Transactions (`COMMIT`, `ROLLBACK`)
- Exception Handling
- Building a Menu-Driven Student Management System
- Mini Project using Python + MySQL
- GUI Integration (Tkinter)
- Exporting Data (CSV/Excel)
