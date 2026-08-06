# Python Full Stack Foundation

# Week-06 – Day-29

# Program-5

# AVG()

## What does it do?

`AVG()` calculates the average value of a numeric column.

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

Display the average marks of all students.

---

## Complete Code

```python
import sqlite3

# Connect to database
connection = sqlite3.connect("college.db")

# Create cursor
cursor = connection.cursor()

# Delete table if exists
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

# Calculate average marks
cursor.execute("""
SELECT AVG(marks)
FROM Student
""")

average = cursor.fetchone()[0]

print("Average Marks :", round(average,2))

# Close connection
connection.close()
```

---

## Output

```
Average Marks : 85.4
```

---

# Program-6

# MIN()

## What does it do?

`MIN()` returns the smallest value from a numeric column.

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

Display the lowest marks scored by a student.

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

# Find minimum marks
cursor.execute("""
SELECT MIN(marks)
FROM Student
""")

minimum = cursor.fetchone()[0]

print("Lowest Marks :", minimum)

# Close connection
connection.close()
```

---

## Output

```
Lowest Marks : 75
```

---

# Program-7

# MAX()

## What does it do?

`MAX()` returns the highest value from a numeric column.

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

Display the highest marks scored by a student.

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

# Find maximum marks
cursor.execute("""
SELECT MAX(marks)
FROM Student
""")

maximum = cursor.fetchone()[0]

print("Highest Marks :", maximum)

# Close connection
connection.close()
```

---

## Output

```
Highest Marks : 94
```

---

# Program-8

# DISTINCT

## What does it do?

`DISTINCT` removes duplicate values and displays only unique records from a column.

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

Display all unique departments.

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

# Display unique departments
cursor.execute("""
SELECT DISTINCT department
FROM Student
""")

departments = cursor.fetchall()

print("Unique Departments")

for department in departments:
    print(department[0])

# Close connection
connection.close()
```

---

## Output

```
Unique Departments

CSE
ECE
IT
```

---

# Summary

In these programs, we learned:

- ✅ AVG()
- ✅ MIN()
- ✅ MAX()
- ✅ DISTINCT

Each program is completely independent.

Every program:

- Creates the table
- Inserts sample data
- Executes the SQL query
- Displays the output
- Closes the database connection
