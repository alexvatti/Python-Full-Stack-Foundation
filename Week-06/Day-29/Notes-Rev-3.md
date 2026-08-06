# Python Full Stack Foundation

# Week-06 – Day-29

# Program-9

# LIKE (Starts With)

## What does it do?

`LIKE 'A%'` displays all records where the value starts with the specified character.

---

## Sample Table

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|
|2|John|ECE|85|
|3|Ravi|CSE|75|
|4|Priya|IT|94|
|5|Anil|ECE|82|

---

## We Want

Display students whose names start with **A**.

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
    ("Anil","ECE",82)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("""
SELECT *
FROM Student
WHERE name LIKE 'A%'
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
(5, 'Anil', 'ECE', 82)
```

---

# Program-10

# LIKE (Ends With)

## What does it do?

`LIKE '%a'` displays all records where the value ends with the specified character.

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

Display students whose names end with **a**.

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

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","CSE",75),
("Priya","IT",94),
("Neha","ECE",82)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("""
SELECT *
FROM Student
WHERE name LIKE '%a'
""")

rows=cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
(4, 'Priya', 'IT', 94)
(5, 'Neha', 'ECE', 82)
```

---

# Program-11

# LIKE (Contains)

## What does it do?

`LIKE '%ri%'` displays all records containing the given text anywhere in the value.

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

Display students whose names contain **ri**.

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

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","CSE",75),
("Priya","IT",94),
("Neha","ECE",82)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("""
SELECT *
FROM Student
WHERE name LIKE '%ri%'
""")

rows=cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
(4, 'Priya', 'IT', 94)
```

---

# Program-12

# LIKE (_ Wildcard)

## What does it do?

`_` (underscore) represents exactly **one character**.

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

Display students whose names match **_lex**.

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

students=[
("Alex","CSE",91),
("John","ECE",85),
("Ravi","CSE",75),
("Priya","IT",94),
("Neha","ECE",82)
]

cursor.executemany("""
INSERT INTO Student(name,department,marks)
VALUES(?,?,?)
""",students)

connection.commit()

cursor.execute("""
SELECT *
FROM Student
WHERE name LIKE '_lex'
""")

rows=cursor.fetchall()

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
(1, 'Alex', 'CSE', 91)
```

---

# Summary

In these four programs, we learned:

- ✅ LIKE 'A%' (Starts With)
- ✅ LIKE '%a' (Ends With)
- ✅ LIKE '%ri%' (Contains)
- ✅ LIKE '_lex' (Single Character Wildcard)

Each program is completely independent and includes:

- Creating the table
- Inserting sample data
- Executing the SQL query
- Displaying the output
- Closing the database connection
