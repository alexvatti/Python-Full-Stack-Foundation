# Python Full Stack Foundation

# Week-06 – Day-29

# Program-1

# COUNT(*)

## What does it do?

`COUNT(*)` returns the total number of records available in a table.

---

## Sample Table

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|
|2|John|ECE|85|
|3|Ravi|CSE|75|
|4|Priya|IT|94|
|5|Neha|ECE|82|

---

## We Want

Display the total number of students.

---

## Complete Code

```python
import sqlite3

# Connect to database
connection = sqlite3.connect("college.db")

# Create cursor
cursor = connection.cursor()

# Delete table if already exists
cursor.execute("DROP TABLE IF EXISTS Student")

# Create Student table
cursor.execute("""
CREATE TABLE Student(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    department TEXT,
    marks INTEGER
)
""")

# Insert records
students = [
    ("Alex","CSE",91),
    ("John","ECE",85),
    ("Ravi","CSE",75),
    ("Priya","IT",94),
    ("Neha","ECE",82)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""", students)

connection.commit()

# COUNT(*)
cursor.execute("""
SELECT COUNT(*)
FROM Student
""")

total = cursor.fetchone()[0]

print("Total Students :", total)

# Close database
connection.close()
```

---

## Output

```
Total Students : 5
```

---

# Program-2

# COUNT(Column)

## What does it do?

`COUNT(column_name)` counts only the non-NULL values in a specific column.

---

## Sample Table

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|
|2|John|ECE|85|
|3|Ravi|CSE|75|
|4|Priya|IT|94|
|5|Neha|ECE|82|

---

## We Want

Count the total number of student names.

---

## Complete Code

```python
import sqlite3

# Connect to database
connection = sqlite3.connect("college.db")

# Create cursor
cursor = connection.cursor()

# Delete table
cursor.execute("DROP TABLE IF EXISTS Student")

# Create table
cursor.execute("""
CREATE TABLE Student(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    department TEXT,
    marks INTEGER
)
""")

# Insert records
students = [
    ("Alex","CSE",91),
    ("John","ECE",85),
    ("Ravi","CSE",75),
    ("Priya","IT",94),
    ("Neha","ECE",82)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""", students)

connection.commit()

# COUNT(name)
cursor.execute("""
SELECT COUNT(name)
FROM Student
""")

total = cursor.fetchone()[0]

print("Total Student Names :", total)

# Close database
connection.close()
```

---

## Output

```
Total Student Names : 5
```

---

# Program-3

# COUNT(DISTINCT)

## What does it do?

`COUNT(DISTINCT column_name)` counts only the unique values in a column.

---

## Sample Table

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|
|2|John|ECE|85|
|3|Ravi|CSE|75|
|4|Priya|IT|94|
|5|Neha|ECE|82|

---

## We Want

Display the total number of unique departments.

---

## Complete Code

```python
import sqlite3

# Connect to database
connection = sqlite3.connect("college.db")

# Create cursor
cursor = connection.cursor()

# Delete old table
cursor.execute("DROP TABLE IF EXISTS Student")

# Create table
cursor.execute("""
CREATE TABLE Student(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    department TEXT,
    marks INTEGER
)
""")

# Insert records
students = [
    ("Alex","CSE",91),
    ("John","ECE",85),
    ("Ravi","CSE",75),
    ("Priya","IT",94),
    ("Neha","ECE",82)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""", students)

connection.commit()

# COUNT DISTINCT
cursor.execute("""
SELECT COUNT(DISTINCT department)
FROM Student
""")

departments = cursor.fetchone()[0]

print("Unique Departments :", departments)

# Close database
connection.close()
```

---

## Output

```
Unique Departments : 3
```

---

## Explanation

Departments available are

```
CSE
ECE
IT
```

Total Unique Departments = **3**

---

# Program-4

# SUM()

## What does it do?

`SUM()` adds all the numeric values in a column.

---

## Sample Table

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|
|2|John|ECE|85|
|3|Ravi|CSE|75|
|4|Priya|IT|94|
|5|Neha|ECE|82|

---

## We Want

Display the total marks of all students.

---

## Complete Code

```python
import sqlite3

# Connect to database
connection = sqlite3.connect("college.db")

# Create cursor
cursor = connection.cursor()

# Delete old table
cursor.execute("DROP TABLE IF EXISTS Student")

# Create table
cursor.execute("""
CREATE TABLE Student(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    department TEXT,
    marks INTEGER
)
""")

# Insert records
students = [
    ("Alex","CSE",91),
    ("John","ECE",85),
    ("Ravi","CSE",75),
    ("Priya","IT",94),
    ("Neha","ECE",82)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""", students)

connection.commit()

# SUM
cursor.execute("""
SELECT SUM(marks)
FROM Student
""")

total_marks = cursor.fetchone()[0]

print("Total Marks :", total_marks)

# Close database
connection.close()
```

---

## Output

```
Total Marks : 427
```

---

# Summary

In these four programs, we learned:

- ✅ COUNT(*)
- ✅ COUNT(column)
- ✅ COUNT(DISTINCT column)
- ✅ SUM(column)

Each program is completely independent and can be copied, executed, and tested without relying on any previous program.
