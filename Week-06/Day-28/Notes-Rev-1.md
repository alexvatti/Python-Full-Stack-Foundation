# Python Full Stack Foundation

# Week-06 – Day-28 Practice Programs

# SQLite SELECT Operations

## 10 Complete Programs

Each program is independent.
Every program:
- Creates the database connection
- Creates the table
- Inserts sample data
- Performs the SELECT operation
- Displays the output
- Closes the database

---

# Program-1

# SELECT All Records

## Table

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|
|2|John|ECE|85|
|3|Ravi|EEE|78|
|4|Priya|CSE|95|

## Operation

Display all students.

## Code

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
    ("Ravi","EEE",78),
    ("Priya","CSE",95)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""", students)

connection.commit()

cursor.execute("SELECT * FROM Student")

rows = cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

## Output

```
(1, 'Alex', 'CSE', 91)
(2, 'John', 'ECE', 85)
(3, 'Ravi', 'EEE', 78)
(4, 'Priya', 'CSE', 95)
```

---

# Program-2

# SELECT Specific Columns

## Operation

Display only Name and Marks.

## Code

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
    ("Ravi","EEE",78),
    ("Priya","CSE",95)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""", students)

connection.commit()

cursor.execute("""
SELECT name, marks
FROM Student
""")

rows = cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

## Output

```
('Alex', 91)
('John', 85)
('Ravi', 78)
('Priya', 95)
```

---

# Program-3

# SELECT using WHERE

## Operation

Display CSE students.

## Code

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

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","EEE",78),
("Priya","CSE",95)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("""
SELECT *
FROM Student
WHERE department='CSE'
""")

rows=cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

## Output

```
(1, 'Alex', 'CSE', 91)
(4, 'Priya', 'CSE', 95)
```

---

# Program-4

# WHERE with Greater Than

## Operation

Display students scoring above 80.

## Code

```python
import sqlite3

connection=sqlite3.connect("college.db")
cursor=connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
department TEXT,
marks INTEGER
)
""")

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","EEE",78),
("Priya","CSE",95)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("""
SELECT *
FROM Student
WHERE marks>80
""")

rows=cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

## Output

```
(1, 'Alex', 'CSE', 91)
(2, 'John', 'ECE', 85)
(4, 'Priya', 'CSE', 95)
```

---

# Program-5

# ORDER BY Ascending

## Operation

Sort students by marks.

## Code

```python
import sqlite3

connection=sqlite3.connect("college.db")
cursor=connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
department TEXT,
marks INTEGER
)
""")

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","EEE",78),
("Priya","CSE",95)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("""
SELECT *
FROM Student
ORDER BY marks
""")

rows=cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

## Output

```
(3, 'Ravi', 'EEE', 78)
(2, 'John', 'ECE', 85)
(1, 'Alex', 'CSE', 91)
(4, 'Priya', 'CSE', 95)
```

---

# Program-6

# ORDER BY Descending

## Operation

Highest marks first.

## Code

```python
import sqlite3

connection=sqlite3.connect("college.db")
cursor=connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
department TEXT,
marks INTEGER
)
""")

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","EEE",78),
("Priya","CSE",95)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("""
SELECT *
FROM Student
ORDER BY marks DESC
""")

rows=cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

## Output

```
(4, 'Priya', 'CSE', 95)
(1, 'Alex', 'CSE', 91)
(2, 'John', 'ECE', 85)
(3, 'Ravi', 'EEE', 78)
```

---

# Program-7

# LIMIT

## Operation

Display first two students.

## Code

```python
import sqlite3

connection=sqlite3.connect("college.db")
cursor=connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
department TEXT,
marks INTEGER
)
""")

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","EEE",78),
("Priya","CSE",95)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("""
SELECT *
FROM Student
LIMIT 2
""")

rows=cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

## Output

```
(1, 'Alex', 'CSE', 91)
(2, 'John', 'ECE', 85)
```

---

# Program-8

# fetchone()

## Operation

Read one record.

## Code

```python
import sqlite3

connection=sqlite3.connect("college.db")
cursor=connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
department TEXT,
marks INTEGER
)
""")

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","EEE",78),
("Priya","CSE",95)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("SELECT * FROM Student")

row=cursor.fetchone()

print(row)

connection.close()
```

## Output

```
(1, 'Alex', 'CSE', 91)
```

---

# Program-9

# fetchmany()

## Operation

Read first three records.

## Code

```python
import sqlite3

connection=sqlite3.connect("college.db")
cursor=connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
department TEXT,
marks INTEGER
)
""")

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","EEE",78),
("Priya","CSE",95)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("SELECT * FROM Student")

rows=cursor.fetchmany(3)

for row in rows:
    print(row)

connection.close()
```

## Output

```
(1, 'Alex', 'CSE', 91)
(2, 'John', 'ECE', 85)
(3, 'Ravi', 'EEE', 78)
```

---

# Program-10

# fetchall()

## Operation

Read all records.

## Code

```python
import sqlite3

connection=sqlite3.connect("college.db")
cursor=connection.cursor()

cursor.execute("DROP TABLE IF EXISTS Student")

cursor.execute("""
CREATE TABLE Student(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
department TEXT,
marks INTEGER
)
""")

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","EEE",78),
("Priya","CSE",95)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("SELECT * FROM Student")

rows=cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

## Output

```
(1, 'Alex', 'CSE', 91)
(2, 'John', 'ECE', 85)
(3, 'Ravi', 'EEE', 78)
(4, 'Priya', 'CSE', 95)
```

---

# Summary

These 10 programs covered:

- SELECT *
- SELECT specific columns
- WHERE clause
- WHERE with comparison operators
- ORDER BY ASC
- ORDER BY DESC
- LIMIT
- fetchone()
- fetchmany()
- fetchall()

Each program is self-contained and can be executed independently.
