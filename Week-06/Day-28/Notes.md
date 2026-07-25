# Python Full Stack Foundation

# Week-06 – Day-28

# SQLite Database Programming

# CRUD Operations (INSERT, SELECT, UPDATE, DELETE)

**Level:** Beginner → Intermediate

**Duration:** 2–3 Hours

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand CRUD Operations
- Insert Records
- Read Records
- Update Records
- Delete Records
- Retrieve Data using SELECT
- Use WHERE Clause
- Use ORDER BY
- Use LIMIT
- Fetch Data using fetchone(), fetchmany(), fetchall()
- Use Parameterized Queries
- Understand SQL Injection (Introduction)

---

# Agenda

1. CRUD Operations
2. INSERT
3. SELECT
4. fetchone()
5. fetchmany()
6. fetchall()
7. WHERE
8. ORDER BY
9. LIMIT
10. UPDATE
11. DELETE
12. Parameterized Queries
13. SQL Injection

---

# Recap

Previous Session

✓ Cursor Object

✓ execute()

✓ commit()

✓ rollback()

✓ close()

✓ CREATE TABLE

✓ PRIMARY KEY

✓ AUTOINCREMENT

Today we will work with table data.

---

# What is CRUD?

CRUD represents the four basic database operations.

```
CRUD

│

├── Create

├── Read

├── Update

└── Delete
```

---

# CRUD Meaning

| Operation | SQL Command |
|------------|-------------|
| Create | INSERT |
| Read | SELECT |
| Update | UPDATE |
| Delete | DELETE |

---

# Real World Example

Student Management System

```
Add Student

↓

View Student

↓

Update Student

↓

Delete Student
```

These are CRUD operations.

---

# Sample Student Table

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|
|2|John|ECE|85|
|3|Ravi|EEE|78|

---

# INSERT Statement

## Definition

INSERT adds new records into a table.

---

# Syntax

```sql
INSERT INTO table_name
VALUES (...);
```

---

# Example

```sql
INSERT INTO Student
VALUES
(1,'Alex','CSE',91);
```

---

# Python Example

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("""

INSERT INTO Student

(name,department,marks)

VALUES

('Alex','CSE',91)

""")

connection.commit()

connection.close()
```

---

# Why Skip ID?

ID uses

```
AUTOINCREMENT
```

SQLite automatically generates it.

---

# Output

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|

---

# Insert Another Record

```python
cursor.execute("""

INSERT INTO Student

(name,department,marks)

VALUES

('John','ECE',88)

""")
```

---

# Insert Multiple Records

```python
students=[

("Ravi","EEE",75),

("Priya","CSE",92),

("Neha","IT",86)

]

cursor.executemany("""

INSERT INTO Student

(name,department,marks)

VALUES(?,?,?)

""",students)

connection.commit()
```

---

# executemany()

Instead of

```
INSERT

INSERT

INSERT
```

Use

```
executemany()
```

Faster and cleaner.

---

# SELECT Statement

## Definition

SELECT retrieves data from a table.

---

# Syntax

```sql
SELECT * FROM Student;
```

---

# Python Example

```python
cursor.execute(

"SELECT * FROM Student"

)
```

---

# Fetching Data

After SELECT,

SQLite stores the result.

Python reads it using

- fetchone()
- fetchmany()
- fetchall()

---

# fetchone()

Returns one record.

Example

```python
cursor.execute(

"SELECT * FROM Student"

)

row=cursor.fetchone()

print(row)
```

Output

```
(1,'Alex','CSE',91)
```

---

# Calling Again

```python
print(cursor.fetchone())
```

Output

```
(2,'John','ECE',88)
```

Cursor moves forward.

---

# fetchmany()

Returns multiple rows.

Example

```python
rows=cursor.fetchmany(2)

print(rows)
```

Output

```
[(1,'Alex','CSE',91),

(2,'John','ECE',88)]
```

---

# fetchall()

Returns all remaining rows.

```python
rows=cursor.fetchall()

print(rows)
```

---

# Example

```python
cursor.execute(

"SELECT * FROM Student"

)

students=cursor.fetchall()

for student in students:

    print(student)
```

Output

```
(1,'Alex','CSE',91)

(2,'John','ECE',88)

(3,'Ravi','EEE',75)
```

---

# Display Records Nicely

```python
for student in students:

    print(

        student[0],

        student[1],

        student[2],

        student[3]

    )
```

Output

```
1 Alex CSE 91

2 John ECE 88

3 Ravi EEE 75
```

---

# WHERE Clause

## Definition

WHERE filters records.

---

# Syntax

```sql
SELECT *

FROM Student

WHERE department='CSE';
```

---

# Python Example

```python
cursor.execute("""

SELECT *

FROM Student

WHERE department='CSE'

""")

print(cursor.fetchall())
```

---

# Another Example

Students scoring above 80

```sql
SELECT *

FROM Student

WHERE marks>80;
```

---

# Comparison Operators

| Operator | Meaning |
|-----------|---------|
| = | Equal |
| > | Greater Than |
| < | Less Than |
| >= | Greater Than or Equal |
| <= | Less Than or Equal |
| != | Not Equal |

---

# ORDER BY

## Definition

Sorts data.

---

Ascending

```sql
SELECT *

FROM Student

ORDER BY marks;
```

---

Descending

```sql
SELECT *

FROM Student

ORDER BY marks DESC;
```

---

Python Example

```python
cursor.execute("""

SELECT *

FROM Student

ORDER BY marks DESC

""")

rows=cursor.fetchall()

for row in rows:

    print(row)
```

---

# LIMIT

Returns limited rows.

```sql
SELECT *

FROM Student

LIMIT 3;
```

Output

First three records.

---

# UPDATE Statement

## Definition

UPDATE modifies existing records.

---

# Syntax

```sql
UPDATE Student

SET marks=95

WHERE id=1;
```

---

# Python Example

```python
cursor.execute("""

UPDATE Student

SET marks=95

WHERE id=1

""")

connection.commit()
```

---

# Output

Before

```
Alex

91
```

After

```
Alex

95
```

---

# Update Department

```python
cursor.execute("""

UPDATE Student

SET department='IT'

WHERE id=2

""")

connection.commit()
```

---

# DELETE Statement

## Definition

DELETE removes records.

---

# Syntax

```sql
DELETE

FROM Student

WHERE id=3;
```

---

# Python Example

```python
cursor.execute("""

DELETE

FROM Student

WHERE id=3

""")

connection.commit()
```

---

# Before Delete

| ID | Name |
|----|------|
|1|Alex|
|2|John|
|3|Ravi|

---

# After Delete

| ID | Name |
|----|------|
|1|Alex|
|2|John|

---

# Delete All Records

```sql
DELETE FROM Student;
```

Only records are removed.

The table remains.

---

# Difference

DELETE

↓

Removes Records

Table Exists

---

DROP TABLE

↓

Deletes Table

Everything is removed.

---

# Parameterized Queries

Never combine user input with SQL.

Incorrect

```python
name=input()

sql="SELECT * FROM Student WHERE name='"+name+"'"
```

Dangerous.

---

# Correct Method

```python
name=input("Enter Name : ")

cursor.execute(

"SELECT * FROM Student WHERE name=?",

(name,)

)

print(cursor.fetchall())
```

---

# Why Use Parameters?

Benefits

✓ Safe

✓ Prevents SQL Injection

✓ Cleaner Code

✓ Faster Execution

---

# SQL Injection

Suppose user enters

```text
' OR 1=1 --
```

Bad SQL construction may expose every record.

Parameterized queries prevent this.

---

# Employee Example

Insert

```python
cursor.execute("""

INSERT INTO Employee

(name,salary,department)

VALUES

('David',55000,'HR')

""")
```

---

# Product Example

```python
cursor.execute("""

INSERT INTO Product

(name,price,quantity)

VALUES

('Laptop',65000,5)

""")
```

---

# Bank Example

```python
cursor.execute("""

UPDATE Account

SET balance=25000

WHERE account_id=1

""")
```

---

# Hospital Example

```python
cursor.execute("""

SELECT *

FROM Patient

WHERE disease='Fever'

""")
```

---

# CRUD Workflow

```
Application

↓

INSERT

↓

SELECT

↓

UPDATE

↓

DELETE

↓

Database
```

---

# Complete CRUD Program

```python
import sqlite3

connection=sqlite3.connect("college.db")

cursor=connection.cursor()

cursor.execute("""

INSERT INTO Student

(name,department,marks)

VALUES

('Kiran','IT',90)

""")

connection.commit()

cursor.execute(

"SELECT * FROM Student"

)

students=cursor.fetchall()

for student in students:

    print(student)

connection.close()
```

---

# Best Practices

✓ Always use parameterized queries.

✓ Commit after INSERT, UPDATE and DELETE.

✓ Close database connections.

✓ Use WHERE while updating or deleting.

✓ Test SQL queries before running them.

---

# Common Mistakes

❌ Forgetting commit()

❌ Forgetting WHERE in UPDATE

Example

```sql
UPDATE Student

SET marks=100;
```

All students become 100.

---

❌ Forgetting WHERE in DELETE

```sql
DELETE FROM Student;
```

Every record is deleted.

---

❌ Using string concatenation for SQL.

Always use

```python
?
```

instead.

---

# Summary

Today we learned

✓ CRUD Operations

✓ INSERT

✓ INSERT Multiple Records

✓ executemany()

✓ SELECT

✓ fetchone()

✓ fetchmany()

✓ fetchall()

✓ WHERE

✓ ORDER BY

✓ LIMIT

✓ UPDATE

✓ DELETE

✓ Parameterized Queries

✓ SQL Injection (Introduction)

---

# Coming Next (Day-29)

- Aggregate Functions
- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()
- DISTINCT
- LIKE
- IN
- BETWEEN
- GROUP BY
- HAVING
- Practice SQL Queries
- Mini Database Reports
