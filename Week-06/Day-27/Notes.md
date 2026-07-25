# Python Full Stack Foundation

# Week-06 – Day-27

# SQLite Database Programming

# Creating Tables, Cursor Object and SQL Execution

**Level:** Beginner → Intermediate

**Duration:** 2–3 Hours

---

# Learning Objectives

By the end of this session, you will be able to

- Understand Cursor Objects
- Execute SQL Statements
- Create Tables
- Understand SQLite Data Types
- Use execute()
- Use commit()
- Understand rollback()
- Close Database Connections
- Create Multiple Tables
- View Database Schema
- Understand Primary Keys

---

# Agenda

1. Database Connection
2. Cursor Object
3. execute()
4. commit()
5. rollback()
6. close()
7. SQL Data Types
8. CREATE TABLE
9. Primary Key
10. AUTOINCREMENT
11. sqlite_master
12. PRAGMA table_info()

---

# Recap

Yesterday we learned

- Data
- Information
- Database
- DBMS
- RDBMS
- SQL
- SQLite
- sqlite3 Module
- Creating Database

Today we will create our first database tables.

---

# Database Connection

Every SQLite program follows the same sequence.

```
Python Program

↓

Connect Database

↓

Create Cursor

↓

Execute SQL

↓

Commit Changes

↓

Close Connection
```

---

# General Syntax

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

# SQL Commands

connection.commit()

connection.close()
```

---

# Understanding Each Step

```
sqlite3.connect()

↓

Connect Database

↓

cursor()

↓

Execute SQL

↓

commit()

↓

Save Changes

↓

close()

↓

Release Resources
```

---

# What is a Cursor?

## Definition

A Cursor is an object that allows Python to execute SQL statements and retrieve results from the database.

Think of the cursor as a messenger between Python and SQLite.

---

# Real World Analogy

Imagine

```
Customer

↓

Waiter

↓

Kitchen
```

Customer → Python

Kitchen → Database

Waiter → Cursor

The waiter carries requests to the kitchen and brings back the results.

Similarly,

Cursor sends SQL commands to SQLite and returns the results.

---

# Creating a Cursor

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()
```

---

# Why is Cursor Required?

Without a cursor,

Python cannot execute SQL statements.

Incorrect

```python
connection.execute(...)
```

Recommended

```python
cursor.execute(...)
```

---

# What is execute()?

## Definition

The execute() method sends SQL commands to the SQLite database.

Syntax

```python
cursor.execute(SQL Statement)
```

---

# Example

```python
cursor.execute("SELECT 1")
```

SQLite executes the SQL command.

---

# First SQL Program

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("SELECT 100")

connection.close()
```

This executes a SQL statement successfully.

---

# Database Execution Flow

```
Python

↓

Cursor

↓

SQLite

↓

Result

↓

Cursor

↓

Python
```

---

# What is commit()?

## Definition

commit() permanently saves changes made to the database.

Without commit(),

changes may not be stored.

---

# Example

```python
connection.commit()
```

---

# Real World Analogy

Imagine writing a Word document.

Until you click

```
Save
```

changes may be lost.

commit() works like Save.

---

# When Should commit() Be Used?

Required after

- INSERT
- UPDATE
- DELETE
- CREATE TABLE
- DROP TABLE
- ALTER TABLE

Not required after

```
SELECT
```

because SELECT only reads data.

---

# Example

```python
cursor.execute(SQL)

connection.commit()
```

---

# What Happens Without commit()?

```
INSERT Data

↓

Program Ends

↓

Data Lost
```

Always remember

```
commit()
```

---

# What is rollback()?

## Definition

rollback() cancels changes made after the last commit.

SQLite supports transactions.

---

# Example

```
INSERT Student

↓

Wrong Data

↓

rollback()

↓

Database Returns to Previous State
```

---

# Syntax

```python
connection.rollback()
```

---

# When is rollback() Useful?

- Banking Applications
- Online Payments
- Hospital Systems
- Inventory Systems

If one operation fails,

all previous operations can be cancelled.

---

# What is close()?

## Definition

close() releases the database connection.

Syntax

```python
connection.close()
```

---

# Why Close Connections?

Benefits

- Releases Memory
- Prevents Database Locking
- Improves Performance
- Good Programming Practice

---

# Complete Connection Example

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

print("Connected")

connection.close()

print("Disconnected")
```

Output

```
Connected

Disconnected
```

---

# SQL Data Types

SQLite uses five storage classes.

| Data Type | Purpose |
|------------|----------|
| INTEGER | Whole Numbers |
| REAL | Decimal Numbers |
| TEXT | Strings |
| BLOB | Binary Data |
| NULL | Empty Value |

---

# INTEGER

Stores whole numbers.

Example

```
1

25

500

10000
```

---

# REAL

Stores decimal values.

Example

```
95.50

1250.75

3.14
```

---

# TEXT

Stores

- Names
- Cities
- Emails
- Departments

Example

```
Alex

Python

Hyderabad
```

---

# BLOB

Stores

- Images
- Videos
- Audio
- Binary Files

Usually not used in beginner projects.

---

# NULL

Represents

"No Value"

Example

```
Phone Number

NULL
```

---

# SQLite Type Affinity

Unlike MySQL,

SQLite is flexible.

Example

```
INTEGER

TEXT

REAL
```

SQLite allows more flexibility in stored values.

---

# What is a Table?

## Definition

A Table stores related data in rows and columns.

---

Example

Student

| ID | Name | Marks |
|----|------|--------|
|101|Alex|95|
|102|John|88|

---

# Table Components

```
Student

↓

Rows

↓

Columns

↓

Cells
```

---

# SQL CREATE TABLE

General Syntax

```sql
CREATE TABLE table_name(

column datatype

);
```

---

# Example

```sql
CREATE TABLE Student(

id INTEGER,

name TEXT,

marks REAL

);
```

---

# Executing from Python

```python
cursor.execute("""

CREATE TABLE Student(

id INTEGER,

name TEXT,

marks REAL

)

""")
```

---

# Complete Program

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("""

CREATE TABLE Student(

id INTEGER,

name TEXT,

marks REAL

)

""")

connection.commit()

connection.close()
```

---

# What Happens?

SQLite creates

```
college.db

↓

Student Table
```

---

# IF NOT EXISTS

Suppose the table already exists.

Running CREATE TABLE again produces an error.

Solution

```sql
CREATE TABLE IF NOT EXISTS Student
```

---

# Example

```python
cursor.execute("""

CREATE TABLE IF NOT EXISTS Student(

id INTEGER,

name TEXT,

marks REAL

)

""")
```

Now the program runs safely every time.

---

# Primary Key

## Definition

A Primary Key uniquely identifies every row.

Example

| ID | Name |
|----|------|
|101|Alex|
|102|John|

ID cannot repeat.

---

# Example

```sql
id INTEGER PRIMARY KEY
```

---

# AUTOINCREMENT

Automatically generates numbers.

Example

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
```

Now

```
1

2

3

4

5
```

are created automatically.

---

# Student Table

```python
cursor.execute("""

CREATE TABLE IF NOT EXISTS Student(

id INTEGER PRIMARY KEY AUTOINCREMENT,

name TEXT,

department TEXT,

marks REAL

)

""")
```

---

# Employee Table

```python
cursor.execute("""

CREATE TABLE IF NOT EXISTS Employee(

emp_id INTEGER PRIMARY KEY AUTOINCREMENT,

name TEXT,

salary REAL,

department TEXT

)

""")
```

---

# Product Table

```python
cursor.execute("""

CREATE TABLE IF NOT EXISTS Product(

product_id INTEGER PRIMARY KEY AUTOINCREMENT,

name TEXT,

price REAL,

quantity INTEGER

)

""")
```

---

# Book Table

```python
cursor.execute("""

CREATE TABLE IF NOT EXISTS Book(

book_id INTEGER PRIMARY KEY AUTOINCREMENT,

title TEXT,

author TEXT,

price REAL

)

""")
```

---

# Hospital Table

```python
cursor.execute("""

CREATE TABLE IF NOT EXISTS Patient(

patient_id INTEGER PRIMARY KEY AUTOINCREMENT,

name TEXT,

age INTEGER,

disease TEXT

)

""")
```

---

# Viewing All Tables

SQLite stores metadata in

```
sqlite_master
```

---

Example

```python
cursor.execute("""

SELECT name

FROM sqlite_master

WHERE type='table'

""")
```

---

# Reading Table Names

```python
tables = cursor.fetchall()

print(tables)
```

Output

```
Student

Employee

Book

Product
```

---

# PRAGMA table_info()

Displays table structure.

Example

```python
cursor.execute(

"PRAGMA table_info(Student)"

)

print(cursor.fetchall())
```

Output

```
Column Name

Data Type

Primary Key

NULL

Default Value
```

---

# Database Structure

```
college.db

│

├── Student

├── Employee

├── Product

├── Book

└── Patient
```

---

# Best Practices

✔ Use meaningful table names.

✔ Always use PRIMARY KEY.

✔ Use AUTOINCREMENT where appropriate.

✔ Call commit() after CREATE TABLE.

✔ Close connections.

✔ Use IF NOT EXISTS.

---

# Common Mistakes

❌ Forgetting commit()

❌ Forgetting close()

❌ Misspelling SQL keywords

❌ Missing commas between columns

Incorrect

```sql
id INTEGER

name TEXT
```

Correct

```sql
id INTEGER,

name TEXT
```

---

# Summary

Today we learned

✓ Cursor Object

✓ execute()

✓ commit()

✓ rollback()

✓ close()

✓ SQLite Data Types

✓ CREATE TABLE

✓ PRIMARY KEY

✓ AUTOINCREMENT

✓ IF NOT EXISTS

✓ sqlite_master

✓ PRAGMA table_info()

✓ Creating Multiple Tables

---

# Coming Next (Day-28)

- INSERT
- INSERT Multiple Rows
- SELECT
- fetchone()
- fetchmany()
- fetchall()
- Parameterized Queries
- SQL Injection (Introduction)
- CRUD Operations (Part-1)
