# Python Full Stack Foundation

# Week-06 – Day-30

# Program-1

# PRIMARY KEY

## What does it do?

This program creates a **Student** table with a **Primary Key**.

Each student receives a unique Student ID.

---

## Why do we use Primary Key?

Imagine a college has two students named **Alex**.

| Student ID | Name |
|------------|------|
|1|Alex|
|2|Alex|

Both names are the same.

How can we identify them?

Using **Student ID**.

A Primary Key uniquely identifies every record.

---

## Advantages

- Every record is unique.
- Duplicate IDs are not allowed.
- NULL values are not allowed.
- Faster searching.
- Faster updates.
- Faster deletion.
- Used to create relationships with other tables.

---

## Table Structure

| Column | Data Type |
|----------|-----------|
| student_id | INTEGER PRIMARY KEY AUTOINCREMENT |
| name | TEXT |
| department | TEXT |

---

## We Want

- Create Student table.
- Insert student records.
- Display all students.

---

## Complete Code

```python
import sqlite3

# Connect Database
connection = sqlite3.connect("college.db")

# Create Cursor
cursor = connection.cursor()

# Delete Old Table
cursor.execute("DROP TABLE IF EXISTS Student")

# Create Student Table
cursor.execute("""
CREATE TABLE Student(
    student_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    department TEXT
)
""")

# Insert Records
students = [
    ("Alex","CSE"),
    ("John","ECE"),
    ("Priya","IT"),
    ("Neha","CSE")
]

cursor.executemany("""
INSERT INTO Student(name,department)
VALUES(?,?)
""",students)

connection.commit()

# Display Records
cursor.execute("SELECT * FROM Student")

rows = cursor.fetchall()

print("Student Records")
print("----------------------------")

for row in rows:
    print(row)

# Close Database
connection.close()
```

---

## Output

```
Student Records
----------------------------
(1, 'Alex', 'CSE')
(2, 'John', 'ECE')
(3, 'Priya', 'IT')
(4, 'Neha', 'CSE')
```

---

## Explanation

SQLite automatically generates

```
1
2
3
4
```

because

```
AUTOINCREMENT
```

is used.

We never inserted Student IDs manually.

SQLite created them automatically.

---

## Industry Usage

Primary Keys are used in almost every database table.

Examples

- Student ID
- Employee ID
- Customer ID
- Product ID
- Order ID
- Patient ID

---

# Program-2

# FOREIGN KEY

## What does it do?

This program creates two related tables.

- Department
- Student

Student table stores the Department ID.

Department table stores Department information.

---

## Why do we use Foreign Key?

Without Foreign Key

```
Student

Alex
CSE

John
ECE

Priya
IT
```

Department names repeat again and again.

This causes

- Duplicate Data
- Wasted Storage
- Difficult Updates

Instead,

Store department information only once.

---

## Advantages

- Removes duplicate data.
- Maintains relationships.
- Better database design.
- Easy reporting.
- Maintains data integrity.

---

## Table Design

Department

| Dept ID | Department |
|----------|------------|
|1|CSE|
|2|ECE|
|3|IT|

Student

| Student | Department ID |
|----------|---------------|
|Alex|1|
|John|2|
|Priya|3|

---

## We Want

Create Department table.

Create Student table.

Display both tables.

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("PRAGMA foreign_keys = ON")

cursor.execute("DROP TABLE IF EXISTS Student")
cursor.execute("DROP TABLE IF EXISTS Department")

# Department Table
cursor.execute("""
CREATE TABLE Department(
    dept_id INTEGER PRIMARY KEY AUTOINCREMENT,
    dept_name TEXT
)
""")

# Student Table
cursor.execute("""
CREATE TABLE Student(
    student_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    dept_id INTEGER,
    FOREIGN KEY(dept_id)
    REFERENCES Department(dept_id)
)
""")

# Insert Departments
departments = [
    ("CSE",),
    ("ECE",),
    ("IT",)
]

cursor.executemany("""
INSERT INTO Department(dept_name)
VALUES(?)
""",departments)

# Insert Students
students = [
    ("Alex",1),
    ("John",2),
    ("Priya",3),
    ("Neha",1)
]

cursor.executemany("""
INSERT INTO Student(name,dept_id)
VALUES(?,?)
""",students)

connection.commit()

print("Department Table")
print("----------------")

cursor.execute("SELECT * FROM Department")

for row in cursor.fetchall():
    print(row)

print()

print("Student Table")
print("----------------")

cursor.execute("SELECT * FROM Student")

for row in cursor.fetchall():
    print(row)

connection.close()
```

---

## Output

```
Department Table
----------------
(1, 'CSE')
(2, 'ECE')
(3, 'IT')

Student Table
----------------
(1, 'Alex', 1)
(2, 'John', 2)
(3, 'Priya', 3)
(4, 'Neha', 1)
```

---

## Explanation

Department ID

```
1
```

means

```
CSE
```

Department ID

```
2
```

means

```
ECE
```

Student table stores only the Department ID.

---

## Industry Usage

Foreign Keys are used in

- Banking
- Hospital
- College
- E-Commerce
- Railway Reservation
- ERP Systems

---

# Program-3

# NOT NULL Constraint

## What does it do?

This program prevents empty values from being inserted.

---

## Why do we use NOT NULL?

Some fields are mandatory.

Examples

- Student Name
- Employee Name
- Email
- Mobile Number

These fields should never be empty.

---

## Advantages

- Prevents incomplete records.
- Improves data quality.
- Makes reports reliable.
- Enforces mandatory fields.

---

## Table Structure

| Column | Constraint |
|----------|------------|
| student_id | PRIMARY KEY |
| name | NOT NULL |
| department | TEXT |

---

## We Want

Create Student table.

Insert valid records.

Display all records.

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
    student_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    department TEXT
)
""")

students = [
    ("Alex","CSE"),
    ("John","ECE"),
    ("Priya","IT")
]

cursor.executemany("""
INSERT INTO Student(name,department)
VALUES(?,?)
""",students)

connection.commit()

cursor.execute("SELECT * FROM Student")

rows = cursor.fetchall()

print("Student Records")

print("----------------")

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
Student Records
----------------
(1, 'Alex', 'CSE')
(2, 'John', 'ECE')
(3, 'Priya', 'IT')
```

---

## Note

The following statement will produce an error because the **name** column cannot be NULL.

```python
cursor.execute("""
INSERT INTO Student(name,department)
VALUES(NULL,'CSE')
""")
```

SQLite Error

```
NOT NULL constraint failed
```

---

## Industry Usage

NOT NULL is commonly used for

- Name
- Email
- Password
- Mobile Number
- Date of Birth

---

# Program-4

# UNIQUE Constraint

## What does it do?

Ensures that duplicate values cannot be stored in a column.

---

## Why do we use UNIQUE?

Some information should appear only once.

Examples

- Email Address
- Mobile Number
- Employee Number
- Aadhaar Number
- Passport Number

---

## Advantages

- Prevents duplicate records.
- Improves authentication.
- Maintains data consistency.
- Ensures unique identities.

---

## Table Structure

| Column | Constraint |
|----------|------------|
| student_id | PRIMARY KEY |
| name | TEXT |
| email | UNIQUE |

---

## We Want

Create Student table.

Insert unique email addresses.

Display all records.

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
    student_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    email TEXT UNIQUE
)
""")

students = [
    ("Alex","alex@gmail.com"),
    ("John","john@gmail.com"),
    ("Priya","priya@gmail.com")
]

cursor.executemany("""
INSERT INTO Student(name,email)
VALUES(?,?)
""",students)

connection.commit()

cursor.execute("SELECT * FROM Student")

rows = cursor.fetchall()

print("Student Records")

print("-------------------------")

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
Student Records
-------------------------
(1, 'Alex', 'alex@gmail.com')
(2, 'John', 'john@gmail.com')
(3, 'Priya', 'priya@gmail.com')
```

---

## Note

Trying to insert the same email again

```python
cursor.execute("""
INSERT INTO Student(name,email)
VALUES('David','alex@gmail.com')
""")
```

SQLite Error

```
UNIQUE constraint failed
```

---

## Industry Usage

UNIQUE is widely used for

- Email Address
- Username
- Mobile Number
- Aadhaar Number
- PAN Number
- Passport Number

---

# Summary

In Part-1, we learned:

✅ PRIMARY KEY

✅ FOREIGN KEY

✅ NOT NULL Constraint

✅ UNIQUE Constraint

These constraints form the foundation of relational database design and are used in almost every real-world database application.
