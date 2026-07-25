# Python Full Stack Foundation

# Week-06 – Day-30

# SQLite Database Programming

# Database Relationships, Constraints & Joins

**Level:** Beginner → Intermediate

**Duration:** 2–3 Hours

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Database Design
- Understand Relationships
- Create Primary Keys
- Create Foreign Keys
- Use Constraints
- Understand One-to-One Relationship
- Understand One-to-Many Relationship
- Understand Many-to-Many Relationship
- Create Related Tables
- Perform INNER JOIN
- Perform LEFT JOIN
- Design a complete College Database

---

# Agenda

1. Database Design
2. Primary Key
3. Foreign Key
4. Constraints
5. Relationships
6. One-to-One
7. One-to-Many
8. Many-to-Many
9. JOINs
10. College Database Design

---

# Recap

Previous Session

✓ Aggregate Functions

✓ GROUP BY

✓ HAVING

✓ LIKE

✓ BETWEEN

✓ IN

✓ SQL Reports

Today we move from single tables to **multiple related tables**.

---

# Why Multiple Tables?

Suppose we store everything in one table.

| Student | Department | Teacher | Course | Marks |
|---------|------------|----------|---------|------:|
|Alex|CSE|Ravi|Python|91|
|Alex|CSE|Ravi|SQL|88|
|Alex|CSE|Ravi|Java|85|

Notice

- Student name repeats.
- Department repeats.
- Teacher repeats.

This causes **Data Redundancy**.

---

# Better Design

Separate tables.

```
Student

Department

Teacher

Course

Enrollment
```

Tables are connected using **relationships**.

---

# What is Database Design?

## Definition

Database Design is the process of organizing data into tables and defining relationships between them.

A good design

- Reduces duplication
- Improves performance
- Maintains consistency
- Simplifies queries

---

# What is a Primary Key?

## Definition

A Primary Key uniquely identifies each row in a table.

Rules

- Cannot be NULL
- Cannot be duplicated
- Should be stable

---

# Example

```sql
CREATE TABLE Student(

id INTEGER PRIMARY KEY AUTOINCREMENT,

name TEXT,

department TEXT

);
```

---

# Why Primary Key?

| ID | Name |
|----|------|
|1|Alex|
|2|John|
|3|Priya|

Even if two students have the same name,

ID remains unique.

---

# What is a Foreign Key?

## Definition

A Foreign Key is a column that refers to the Primary Key of another table.

It creates a relationship between tables.

---

# Visual Representation

```
Department

+----+------+

| 1  | CSE  |

| 2  | ECE  |

+----+------+

       ↑

       |

Student.department_id
```

---

# Department Table

```sql
CREATE TABLE Department(

dept_id INTEGER PRIMARY KEY AUTOINCREMENT,

dept_name TEXT UNIQUE

);
```

---

# Student Table

```sql
CREATE TABLE Student(

student_id INTEGER PRIMARY KEY AUTOINCREMENT,

name TEXT,

department_id INTEGER,

FOREIGN KEY (department_id)

REFERENCES Department(dept_id)

);
```

---

# Relationship Meaning

If a student has

```
department_id = 1
```

then that student belongs to

```
Department 1 → CSE
```

---

# Enabling Foreign Keys in SQLite

SQLite requires

```python
cursor.execute("PRAGMA foreign_keys = ON")
```

Always enable this after connecting.

---

# What are Constraints?

## Definition

Constraints are rules applied to table columns to maintain data integrity.

---

# Common Constraints

| Constraint | Purpose |
|------------|---------|
| PRIMARY KEY | Unique row |
| FOREIGN KEY | Relationship |
| NOT NULL | Value required |
| UNIQUE | No duplicates |
| CHECK | Custom validation |
| DEFAULT | Automatic value |

---

# NOT NULL

```sql
name TEXT NOT NULL
```

Name cannot be empty.

---

# UNIQUE

```sql
email TEXT UNIQUE
```

Duplicate emails are not allowed.

---

# CHECK

```sql
marks REAL CHECK(marks>=0 AND marks<=100)
```

Marks must be between 0 and 100.

---

# DEFAULT

```sql
status TEXT DEFAULT 'ACTIVE'
```

If no value is provided,

SQLite stores

```
ACTIVE
```

---

# Complete Table Example

```sql
CREATE TABLE Student(

student_id INTEGER PRIMARY KEY AUTOINCREMENT,

name TEXT NOT NULL,

email TEXT UNIQUE,

marks REAL CHECK(marks>=0 AND marks<=100),

status TEXT DEFAULT 'ACTIVE'

);
```

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

## Definition

One record in Table A is related to one record in Table B.

---

# Example

Student ↔ StudentIDCard

| Student | ID Card |
|---------|---------|
|Alex|CARD101|
|John|CARD102|

One student has one card.

One card belongs to one student.

---

# Table Design

```sql
CREATE TABLE Student(

student_id INTEGER PRIMARY KEY,

name TEXT

);

CREATE TABLE IDCard(

card_id INTEGER PRIMARY KEY,

student_id INTEGER UNIQUE,

FOREIGN KEY(student_id)

REFERENCES Student(student_id)

);
```

`UNIQUE` ensures one card per student.

---

# One-to-Many Relationship

## Definition

One record in Table A can relate to many records in Table B.

---

# Most Common Relationship

Department → Students

```
CSE

├── Alex

├── Priya

└── Kiran
```

One department has many students.

Each student belongs to one department.

---

# Table Design

```sql
CREATE TABLE Department(

dept_id INTEGER PRIMARY KEY,

dept_name TEXT

);

CREATE TABLE Student(

student_id INTEGER PRIMARY KEY,

name TEXT,

dept_id INTEGER,

FOREIGN KEY(dept_id)

REFERENCES Department(dept_id)

);
```

---

# Many-to-Many Relationship

## Definition

Many records in Table A can relate to many records in Table B.

---

# Example

Students and Courses.

| Student | Course |
|---------|--------|
|Alex|Python|
|Alex|SQL|
|John|Python|
|John|Java|

A student can take many courses.

A course can have many students.

---

# Solution: Junction Table

```
Student

Course

Enrollment
```

---

# Student Table

```sql
CREATE TABLE Student(

student_id INTEGER PRIMARY KEY,

name TEXT

);
```

---

# Course Table

```sql
CREATE TABLE Course(

course_id INTEGER PRIMARY KEY,

course_name TEXT

);
```

---

# Enrollment Table

```sql
CREATE TABLE Enrollment(

student_id INTEGER,

course_id INTEGER,

PRIMARY KEY(student_id,course_id),

FOREIGN KEY(student_id)

REFERENCES Student(student_id),

FOREIGN KEY(course_id)

REFERENCES Course(course_id)

);
```

This is the standard Many-to-Many design.

---

# Inserting Related Data

## Insert Departments

```python
cursor.execute("""

INSERT INTO Department(dept_name)

VALUES ('CSE')

""")

cursor.execute("""

INSERT INTO Department(dept_name)

VALUES ('ECE')

""")
```

---

# Insert Students

```python
cursor.execute("""

INSERT INTO Student(name,department_id)

VALUES ('Alex',1)

""")

cursor.execute("""

INSERT INTO Student(name,department_id)

VALUES ('Priya',1)

""")

cursor.execute("""

INSERT INTO Student(name,department_id)

VALUES ('John',2)

""")

connection.commit()
```

---

# What is a JOIN?

## Definition

A JOIN combines rows from multiple tables based on a relationship.

Without JOIN,

related data stays in separate tables.

With JOIN,

we can see meaningful combined information.

---

# INNER JOIN

Returns only matching records.

---

# Syntax

```sql
SELECT ...

FROM table1

INNER JOIN table2

ON table1.column = table2.column;
```

---

# Example

```sql
SELECT

Student.name,

Department.dept_name

FROM Student

INNER JOIN Department

ON Student.department_id = Department.dept_id;
```

---

# Result

| Student | Department |
|---------|------------|
|Alex|CSE|
|Priya|CSE|
|John|ECE|

---

# Python Example

<CodeBlock language="python" content="cursor.execute(&quot;&quot;&quot;
SELECT
    Student.name,
    Department.dept_name
FROM Student
INNER JOIN Department
ON Student.department_id = Department.dept_id
&quot;&quot;&quot;)

rows = cursor.fetchall()

for row in rows:
    print(row)"/>

---

# LEFT JOIN

Returns

- All records from the left table
- Matching records from the right table

---

# Example

```sql
SELECT

Student.name,

Department.dept_name

FROM Student

LEFT JOIN Department

ON Student.department_id = Department.dept_id;
```

Even students without a department will appear.

---

# INNER JOIN vs LEFT JOIN

| INNER JOIN | LEFT JOIN |
|------------|-----------|
| Only matches | All left records |
| Missing records excluded | Missing records included |

---

# RIGHT JOIN

SQLite does not support RIGHT JOIN directly.

Equivalent logic can be achieved by swapping table order and using LEFT JOIN.

---

# College Database Design

## Tables

```
Department

Teacher

Student

Course

Enrollment

Marks
```

---

# ER-Style Diagram

```text
Department

│

├── Teacher

└── Student

        │

        └── Enrollment

                │

                └── Course
```

---

# Create Department

<CodeBlock language="sql" content="CREATE TABLE Department(
    dept_id INTEGER PRIMARY KEY AUTOINCREMENT,
    dept_name TEXT UNIQUE NOT NULL
);"/>

---

# Create Teacher

<CodeBlock language="sql" content="CREATE TABLE Teacher(
    teacher_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    dept_id INTEGER,
    FOREIGN KEY(dept_id) REFERENCES Department(dept_id)
);"/>

---

# Create Student

<CodeBlock language="sql" content="CREATE TABLE Student(
    student_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT UNIQUE,
    dept_id INTEGER,
    FOREIGN KEY(dept_id) REFERENCES Department(dept_id)
);"/>

---

# Create Course

<CodeBlock language="sql" content="CREATE TABLE Course(
    course_id INTEGER PRIMARY KEY AUTOINCREMENT,
    course_name TEXT NOT NULL,
    teacher_id INTEGER,
    FOREIGN KEY(teacher_id) REFERENCES Teacher(teacher_id)
);"/>

---

# Create Enrollment

<CodeBlock language="sql" content="CREATE TABLE Enrollment(
    student_id INTEGER,
    course_id INTEGER,
    enrollment_date TEXT DEFAULT CURRENT_DATE,
    PRIMARY KEY(student_id,course_id),
    FOREIGN KEY(student_id) REFERENCES Student(student_id),
    FOREIGN KEY(course_id) REFERENCES Course(course_id)
);"/>

---

# Useful Report Query

Student + Department + Course

<CodeBlock language="sql" content="SELECT
    s.name AS Student,
    d.dept_name AS Department,
    c.course_name AS Course
FROM Student s
JOIN Department d ON s.dept_id = d.dept_id
JOIN Enrollment e ON s.student_id = e.student_id
JOIN Course c ON e.course_id = c.course_id;"/>

---

# Database Design Best Practices

## 1. Use Singular or Consistent Table Names

Good

- Student
- Department
- Course

---

## 2. Always Define Primary Keys

Every table should have a unique identifier.

---

## 3. Use Foreign Keys for Relationships

This maintains referential integrity.

---

## 4. Avoid Duplicate Data

Store information once.

Reference it using keys.

---

## 5. Use Meaningful Column Names

Good

- student_id
- course_name
- department_id

Bad

- s
- c
- d1

---

# Common Mistakes

## Forgetting Foreign Keys

Tables become disconnected.

---

## Using Text Instead of IDs

Bad

```sql
department_name TEXT
```

Better

```sql
department_id INTEGER
```

---

## No Constraints

Invalid data enters the database.

Example

```
Marks = 500
```

---

## Duplicate Records

Without UNIQUE,

the same email can be inserted multiple times.

---

# Full Workflow

```
Design Tables

↓

Define Primary Keys

↓

Define Foreign Keys

↓

Insert Master Data

↓

Insert Related Data

↓

Use JOINs

↓

Generate Reports
```

---

# Summary

Today we learned

✓ Database Design

✓ Primary Key

✓ Foreign Key

✓ Constraints

✓ NOT NULL

✓ UNIQUE

✓ CHECK

✓ DEFAULT

✓ One-to-One Relationship

✓ One-to-Many Relationship

✓ Many-to-Many Relationship

✓ Junction Tables

✓ INNER JOIN

✓ LEFT JOIN

✓ College Database Design

✓ Report Queries

---

# Coming Next (Week-07 Day-31)

Transition from SQLite to MySQL

- Installing MySQL
- MySQL Server vs SQLite
- MySQL Workbench
- Connecting to localhost
- Creating databases in MySQL
- Running SQL in MySQL Workbench
- Migrating SQLite concepts to MySQL
- Client-Server Database Architecture
