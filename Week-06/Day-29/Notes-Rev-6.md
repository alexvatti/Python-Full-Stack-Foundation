# Python Full Stack Foundation

# Week-06 – Day-29

# Program-21

# GROUP BY + HAVING

## What does it do?

`GROUP BY` groups similar records together.

`HAVING` filters the grouped records.

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

Display departments whose **average marks are greater than 85**.

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

# Display departments whose average marks are greater than 85
cursor.execute("""
SELECT
department,
AVG(marks)
FROM Student
GROUP BY department
HAVING AVG(marks) > 85
""")

rows = cursor.fetchall()

print("Department   Average Marks")
print("--------------------------")

for row in rows:
    print(row[0], "\t", round(row[1],2))

# Close connection
connection.close()
```

---

## Output

```
Department   Average Marks
--------------------------
IT           94.0
```

---

# Program-22

# Complete Dashboard Report

## What does it do?

Generates a complete department-wise report using multiple aggregate functions.

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

Display

- Department
- Total Students
- Average Marks
- Lowest Marks
- Highest Marks

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

# Generate Dashboard Report
cursor.execute("""
SELECT
department,
COUNT(*),
AVG(marks),
MIN(marks),
MAX(marks)
FROM Student
GROUP BY department
""")

rows = cursor.fetchall()

print("Department  Students  Average  Lowest  Highest")
print("------------------------------------------------")

for row in rows:
    print(
        row[0],
        "\t",
        row[1],
        "\t",
        round(row[2],2),
        "\t",
        row[3],
        "\t",
        row[4]
    )

# Close connection
connection.close()
```

---

## Output

```
Department  Students  Average  Lowest  Highest
------------------------------------------------
CSE         2         83.0     75      91
ECE         2         83.5     82      85
IT          1         94.0     94      94
```

---

# Summary

Congratulations! 🎉

You have completed all **22 SQLite SELECT Practice Programs**.

### Topics Covered

✅ COUNT(*)

✅ COUNT(column)

✅ COUNT(DISTINCT)

✅ SUM()

✅ AVG()

✅ MIN()

✅ MAX()

✅ DISTINCT

✅ LIKE (Starts With)

✅ LIKE (Ends With)

✅ LIKE (Contains)

✅ LIKE (_ Wildcard)

✅ BETWEEN

✅ IN

✅ NOT IN

✅ GROUP BY

✅ GROUP BY + COUNT()

✅ GROUP BY + AVG()

✅ GROUP BY + SUM()

✅ HAVING

✅ GROUP BY + HAVING

✅ Complete Dashboard Report

---

These 22 programs form a complete beginner-to-intermediate practice workbook for SQLite SELECT queries using Python.
