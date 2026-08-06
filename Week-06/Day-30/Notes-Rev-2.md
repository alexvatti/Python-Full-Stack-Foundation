# Python Full Stack Foundation

# Week-06 – Day-30

# Part-2

# Program-5

# CHECK Constraint

## What does it do?

The **CHECK** constraint allows only valid data to be inserted into a table.

If the condition is not satisfied, SQLite rejects the record.

---

## Why do we use CHECK?

Imagine storing student marks.

Valid Marks

```
0 - 100
```

Invalid Marks

```
-15

120

250
```

A CHECK constraint prevents such invalid data.

---

## Advantages

- Prevents invalid data
- Improves data quality
- Automatic validation
- Reduces programming effort
- Maintains database consistency

---

## Table Structure

| Column | Constraint |
|----------|------------|
| student_id | PRIMARY KEY |
| name | TEXT |
| marks | CHECK(marks>=0 AND marks<=100) |

---

## We Want

- Create Student table
- Insert valid student records
- Display all records

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
    marks INTEGER CHECK(marks>=0 AND marks<=100)
)
""")

students = [
    ("Alex",91),
    ("John",85),
    ("Priya",95)
]

cursor.executemany("""
INSERT INTO Student(name,marks)
VALUES(?,?)
""", students)

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
(1, 'Alex', 91)
(2, 'John', 85)
(3, 'Priya', 95)
```

---

## Invalid Example

```python
cursor.execute("""
INSERT INTO Student(name,marks)
VALUES('David',120)
""")
```

SQLite Error

```
CHECK constraint failed
```

---

## Industry Usage

CHECK constraints are used for

- Student Marks
- Product Price
- Employee Age
- Salary
- Rating
- Quantity

---

# Program-6

# DEFAULT Constraint

## What does it do?

The **DEFAULT** constraint automatically inserts a value if the user does not provide one.

---

## Why do we use DEFAULT?

Suppose every newly admitted student should have

```
ACTIVE
```

status.

Instead of typing it every time,

SQLite inserts it automatically.

---

## Advantages

- Saves time
- Reduces typing
- Prevents missing values
- Maintains consistency

---

## Table Structure

| Column | Constraint |
|----------|------------|
| student_id | PRIMARY KEY |
| name | TEXT |
| status | DEFAULT 'ACTIVE' |

---

## We Want

Create Student table.

Insert students without giving status.

Display records.

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
    status TEXT DEFAULT 'ACTIVE'
)
""")

students = [
    ("Alex",),
    ("John",),
    ("Priya",)
]

cursor.executemany("""
INSERT INTO Student(name)
VALUES(?)
""", students)

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
(1, 'Alex', 'ACTIVE')
(2, 'John', 'ACTIVE')
(3, 'Priya', 'ACTIVE')
```

---

## Industry Usage

DEFAULT is commonly used for

- ACTIVE Status
- Current Date
- Country
- Quantity = 0
- Balance = 0

---

# Program-7

# One-to-One Relationship

## What does it do?

Creates two related tables.

- Student
- IDCard

Each student receives only one ID Card.

---

## Why do we use One-to-One?

Example

```
Student

↓

One ID Card

↓

One Student
```

One Student

↓

One Aadhaar

One Passport

One PAN Card

---

## Advantages

- Prevents duplicate records
- Better organization
- Easy management
- Maintains unique relationships

---

## We Want

Create Student table.

Create ID Card table.

Display both tables.

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("PRAGMA foreign_keys = ON")

cursor.execute("DROP TABLE IF EXISTS IDCard")
cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
    student_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT
)
""")

cursor.execute("""
CREATE TABLE IDCard(
    card_id INTEGER PRIMARY KEY AUTOINCREMENT,
    card_number TEXT,
    student_id INTEGER UNIQUE,
    FOREIGN KEY(student_id)
    REFERENCES Student(student_id)
)
""")

students = [
    ("Alex",),
    ("John",),
    ("Priya",)
]

cursor.executemany("""
INSERT INTO Student(name)
VALUES(?)
""", students)

cards = [
    ("CARD101",1),
    ("CARD102",2),
    ("CARD103",3)
]

cursor.executemany("""
INSERT INTO IDCard(card_number,student_id)
VALUES(?,?)
""", cards)

connection.commit()

print("Student Table")
print("----------------")

cursor.execute("SELECT * FROM Student")

for row in cursor.fetchall():
    print(row)

print()

print("ID Card Table")
print("----------------")

cursor.execute("SELECT * FROM IDCard")

for row in cursor.fetchall():
    print(row)

connection.close()
```

---

## Output

```
Student Table
----------------
(1, 'Alex')
(2, 'John')
(3, 'Priya')

ID Card Table
----------------
(1, 'CARD101', 1)
(2, 'CARD102', 2)
(3, 'CARD103', 3)
```

---

## Industry Usage

One-to-One relationships are used for

- Student ↔ ID Card
- Employee ↔ Passport
- Citizen ↔ Aadhaar
- Vehicle ↔ Registration

---

# Program-8

# One-to-Many Relationship

## What does it do?

Creates Department and Student tables.

One department contains many students.

Each student belongs to only one department.

---

## Why do we use One-to-Many?

Example

```
CSE

↓

Alex

↓

Priya

↓

Kiran
```

One Department

↓

Many Students

---

## Advantages

- Most common relationship
- Eliminates duplicate data
- Easy reporting
- Better database design
- Simple maintenance

---

## We Want

Create Department table.

Create Student table.

Display department-wise students using INNER JOIN.

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("PRAGMA foreign_keys = ON")

cursor.execute("DROP TABLE IF EXISTS Student")
cursor.execute("DROP TABLE IF EXISTS Department")

cursor.execute("""
CREATE TABLE Department(
    dept_id INTEGER PRIMARY KEY AUTOINCREMENT,
    dept_name TEXT
)
""")

cursor.execute("""
CREATE TABLE Student(
    student_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    dept_id INTEGER,
    FOREIGN KEY(dept_id)
    REFERENCES Department(dept_id)
)
""")

departments = [
    ("CSE",),
    ("ECE",),
    ("IT",)
]

cursor.executemany("""
INSERT INTO Department(dept_name)
VALUES(?)
""", departments)

students = [
    ("Alex",1),
    ("Priya",1),
    ("John",2),
    ("Neha",3)
]

cursor.executemany("""
INSERT INTO Student(name,dept_id)
VALUES(?,?)
""", students)

connection.commit()

cursor.execute("""
SELECT
Student.student_id,
Student.name,
Department.dept_name
FROM Student
INNER JOIN Department
ON Student.dept_id = Department.dept_id
""")

rows = cursor.fetchall()

print("Student Details")
print("--------------------------------")

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
Student Details
--------------------------------
(1, 'Alex', 'CSE')
(2, 'Priya', 'CSE')
(3, 'John', 'ECE')
(4, 'Neha', 'IT')
```

---

## Industry Usage

One-to-Many relationships are used in

- Department → Students
- Customer → Orders
- Teacher → Subjects
- Doctor → Patients
- Category → Products

---

# Summary

Today we learned

✅ CHECK Constraint

✅ DEFAULT Constraint

✅ One-to-One Relationship

✅ One-to-Many Relationship

These concepts help enforce data validation and build well-structured relational databases used in real-world applications.
