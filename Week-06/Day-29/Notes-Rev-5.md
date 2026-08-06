# Python Full Stack Foundation

# Week-06 – Day-29

# Program-17

# GROUP BY + COUNT()

## What does it do?

`GROUP BY` groups similar records, and `COUNT()` counts the number of records in each group.

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

Display the total number of students in each department.

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

print("Department   Students")
print("----------------------")

for row in rows:
    print(row[0], "\t", row[1])

connection.close()
```

---

## Output

```
Department   Students
----------------------
CSE          2
ECE          2
IT           1
```

---

# Program-18

# GROUP BY + AVG()

## What does it do?

Calculates the average marks of students in each department.

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

Display the average marks for each department.

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
AVG(marks)
FROM Student
GROUP BY department
""")

rows = cursor.fetchall()

print("Department   Average Marks")
print("--------------------------")

for row in rows:
    print(row[0], "\t", round(row[1],2))

connection.close()
```

---

## Output

```
Department   Average Marks
--------------------------
CSE          83.0
ECE          83.5
IT           94.0
```

---

# Program-19

# GROUP BY + SUM()

## What does it do?

Calculates the total marks obtained by students in each department.

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

Display the total marks department-wise.

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
SUM(marks)
FROM Student
GROUP BY department
""")

rows = cursor.fetchall()

print("Department   Total Marks")
print("------------------------")

for row in rows:
    print(row[0], "\t", row[1])

connection.close()
```

---

## Output

```
Department   Total Marks
------------------------
CSE          166
ECE          167
IT           94
```

---

# Program-20

# HAVING Clause

## What does it do?

`HAVING` filters grouped records after `GROUP BY`.

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

Display only those departments having more than one student.

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
HAVING COUNT(*) > 1
""")

rows = cursor.fetchall()

print("Departments having more than one student")

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
Departments having more than one student

('CSE', 2)
('ECE', 2)
```

---

# Summary

In these programs, we learned:

- ✅ GROUP BY + COUNT()
- ✅ GROUP BY + AVG()
- ✅ GROUP BY + SUM()
- ✅ HAVING

Each program is completely independent and includes:

- Creating the Student table
- Inserting sample data
- Executing the SQL query
- Displaying the output
- Closing the database connection
