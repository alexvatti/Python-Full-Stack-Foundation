# Python Full Stack Foundation

# Week-06 – Day-29

# Program-13

# BETWEEN

## What does it do?

`BETWEEN` selects records whose values fall within a specified range.

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

Display students who scored between **80 and 90**.

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    department TEXT,
    marks INTEGER
)
""")

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

cursor.execute("""
SELECT *
FROM Student
WHERE marks BETWEEN 80 AND 90
""")

rows = cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
(2, 'John', 'ECE', 85)
(5, 'Neha', 'ECE', 82)
```

---

# Program-14

# IN Operator

## What does it do?

`IN` checks whether a value matches any value in a given list.

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

Display students from **CSE** and **IT** departments.

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    department TEXT,
    marks INTEGER
)
""")

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

cursor.execute("""
SELECT *
FROM Student
WHERE department IN ('CSE','IT')
""")

rows = cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
(1, 'Alex', 'CSE', 91)
(3, 'Ravi', 'CSE', 75)
(4, 'Priya', 'IT', 94)
```

---

# Program-15

# NOT IN Operator

## What does it do?

`NOT IN` returns records that do not belong to the specified list.

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

Display students who are **not** from the **ECE** department.

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    department TEXT,
    marks INTEGER
)
""")

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

cursor.execute("""
SELECT *
FROM Student
WHERE department NOT IN ('ECE')
""")

rows = cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
(1, 'Alex', 'CSE', 91)
(3, 'Ravi', 'CSE', 75)
(4, 'Priya', 'IT', 94)
```

---

# Program-16

# GROUP BY

## What does it do?

`GROUP BY` groups similar records together and performs calculations for each group.

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

Display the number of students in each department.

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    department TEXT,
    marks INTEGER
)
""")

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

cursor.execute("""
SELECT department,
COUNT(*)
FROM Student
GROUP BY department
""")

rows = cursor.fetchall()

print("Department Wise Student Count")

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
Department Wise Student Count

('CSE', 2)
('ECE', 2)
('IT', 1)
```

---

# Summary

In these four programs, we learned:

- ✅ BETWEEN
- ✅ IN
- ✅ NOT IN
- ✅ GROUP BY

Each program is completely independent and includes:

- Creating the Student table
- Inserting sample records
- Executing the SQL query
- Displaying the result
- Closing the database connection
