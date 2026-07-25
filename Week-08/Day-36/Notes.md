# Python Full Stack Foundation

# Week-08 – Day-36

# Python + MySQL Integration

# Connecting Python to MySQL & Executing SQL Queries

**Level:** Beginner → Intermediate

**Duration:** 3 Hours

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Python Database Programming
- Understand Database Connectors
- Install MySQL Connector
- Connect Python to MySQL Server
- Create Database Connections
- Create Cursor Objects
- Execute SQL Statements
- Execute Parameterized Queries
- Fetch Data from MySQL
- Commit Transactions
- Close Connections Properly
- Handle Database Exceptions
- Understand the Python Database API (DB-API)

---

# Agenda

1. Python Database Programming
2. DB-API
3. MySQL Connector
4. Installing Connector
5. Creating Connection
6. Cursor Object
7. Executing SQL
8. Fetching Records
9. Commit & Rollback
10. Exception Handling
11. Best Practices
12. Complete Example

---

# Recap

Previous Week

✓ MySQL Installation

✓ CREATE DATABASE

✓ CREATE TABLE

✓ CRUD Operations

✓ Aggregate Functions

✓ JOINS

✓ Relationships

Today

Python will directly communicate with the MySQL Server.

---

# Why Connect Python to MySQL?

So far

```
Python

↓

Print()

↓

Console
```

Now

```
Python

↓

MySQL Connector

↓

MySQL Server

↓

Database
```

Python programs can now

- Store data
- Read data
- Update data
- Delete data
- Generate reports

---

# Real World Applications

Python + MySQL is used in

- Student Management System
- Banking Applications
- Hospital Management
- HR Systems
- E-Commerce Websites
- Inventory Management
- Employee Payroll
- Attendance Systems

---

# What is a Database Connector?

## Definition

A Database Connector is a software library that allows Python programs to communicate with a database server.

Think of it as a translator between Python and MySQL.

---

# Architecture

```
Python Program

↓

mysql-connector-python

↓

MySQL Server

↓

Database
```

---

# Python DB-API

## Definition

Python Database API (DB-API 2.0) is a standard interface for communicating with relational databases.

Most database libraries follow the same structure.

Examples

```
sqlite3

mysql.connector

psycopg2

cx_Oracle
```

Once you learn one connector, learning others becomes much easier.

---

# Installing MySQL Connector

Open Command Prompt

```bash
pip install mysql-connector-python
```

---

# Verify Installation

```bash
pip show mysql-connector-python
```

---

# Import Module

```python
import mysql.connector
```

If no error occurs,

installation is successful.

---

# Connection Parameters

| Parameter | Description |
|------------|-------------|
| host | Server Name |
| user | Username |
| password | MySQL Password |
| database | Database Name |
| port | MySQL Port (3306) |

---

# Basic Connection

```python
import mysql.connector

connection = mysql.connector.connect(

host="localhost",

user="root",

password="root123",

database="college_db"

)

print("Connected Successfully")
```

---

# Connection Object

The connection object represents the communication channel between Python and MySQL.

```
Python

↓

Connection Object

↓

MySQL Server
```

---

# Check Connection

```python
import mysql.connector

connection = mysql.connector.connect(

host="localhost",

user="root",

password="root123",

database="college_db"

)

if connection.is_connected():

    print("Database Connected")
```

---

# Getting Server Information

```python
print(connection.get_server_info())
```

Example

```
8.0.42
```

---

# Creating Cursor

## Definition

A Cursor is used to execute SQL statements.

```python
cursor = connection.cursor()
```

---

# Why Cursor?

Without Cursor

```
Python

↓

Database
```

Impossible

With Cursor

```
Python

↓

Cursor

↓

Database
```

---

# Executing SQL

```python
cursor.execute(

"SHOW TABLES"

)
```

---

# Fetching Data

```python
tables = cursor.fetchall()

print(tables)
```

Output

```
Student

Department

Employee
```

---

# Display Tables

```python
cursor.execute("SHOW TABLES")

tables = cursor.fetchall()

for table in tables:

    print(table)
```

---

# Executing SELECT Query

```python
cursor.execute(

"SELECT * FROM Student"

)

rows = cursor.fetchall()

for row in rows:

    print(row)
```

---

# fetchone()

Returns one row.

```python
cursor.execute(

"SELECT * FROM Student"

)

print(cursor.fetchone())
```

---

# fetchmany()

Returns limited rows.

```python
rows = cursor.fetchmany(3)

print(rows)
```

---

# fetchall()

Returns every row.

```python
rows = cursor.fetchall()
```

---

# Difference

| Function | Returns |
|-----------|----------|
| fetchone() | One Record |
| fetchmany() | Specified Number |
| fetchall() | All Records |

---

# Executing INSERT

```python
sql = """

INSERT INTO Student

(name,department,marks)

VALUES(%s,%s,%s)

"""

values=("Alex","CSE",91)

cursor.execute(sql,values)

connection.commit()
```

---

# Why %s?

Parameterized Queries prevent SQL Injection.

Never concatenate SQL strings.

Correct

```python
cursor.execute(

sql,

values

)
```

Wrong

```python
sql="SELECT * FROM Student WHERE name='"+name+"'"
```

---

# Executing UPDATE

```python
sql="""

UPDATE Student

SET marks=%s

WHERE student_id=%s

"""

cursor.execute(sql,(95,1))

connection.commit()
```

---

# Executing DELETE

```python
sql="""

DELETE FROM Student

WHERE student_id=%s

"""

cursor.execute(sql,(5,))

connection.commit()
```

---

# Commit

## Definition

COMMIT permanently saves changes.

```python
connection.commit()
```

Required after

- INSERT
- UPDATE
- DELETE

---

# Rollback

## Definition

ROLLBACK cancels uncommitted changes.

```python
connection.rollback()
```

Useful when an error occurs.

---

# Example

```python
try:

    cursor.execute(sql)

    connection.commit()

except:

    connection.rollback()
```

---

# Exception Handling

```python
import mysql.connector

try:

    connection=mysql.connector.connect(

        host="localhost",

        user="root",

        password="root123",

        database="college_db"

    )

    print("Connected")

except mysql.connector.Error as e:

    print("Database Error")

    print(e)
```

---

# Closing Resources

Always close

```python
cursor.close()

connection.close()
```

---

# Why Close Connections?

Benefits

✓ Releases memory

✓ Prevents connection leaks

✓ Improves performance

✓ Frees server resources

---

# Complete Connection Workflow

```
Import Module

↓

Create Connection

↓

Create Cursor

↓

Execute SQL

↓

Fetch Data

↓

Commit

↓

Close Cursor

↓

Close Connection
```

---

# Complete Example

```python
import mysql.connector

connection=mysql.connector.connect(

host="localhost",

user="root",

password="root123",

database="college_db"

)

cursor=connection.cursor()

cursor.execute(

"SELECT * FROM Student"

)

rows=cursor.fetchall()

for row in rows:

    print(row)

cursor.close()

connection.close()
```

---

# Reusable Connection Function

```python
import mysql.connector

def get_connection():

    return mysql.connector.connect(

        host="localhost",

        user="root",

        password="root123",

        database="college_db"

    )
```

Usage

```python
connection=get_connection()

cursor=connection.cursor()
```

---

# Best Practices

✓ Use parameterized queries.

✓ Always commit changes.

✓ Close cursor and connection.

✓ Use try-except blocks.

✓ Keep database credentials in configuration files.

✓ Use meaningful variable names.

---

# Common Errors

### Access Denied

```
1045 Access denied
```

Reason

Wrong username/password.

---

### Unknown Database

```
1049 Unknown database
```

Reason

Database does not exist.

---

### Can't Connect

```
2003 Can't connect
```

Reason

MySQL Server is not running.

---

### Module Not Found

```
ModuleNotFoundError

mysql.connector
```

Reason

Connector not installed.

---

# Complete Program Flow

```
Python

↓

Import Connector

↓

Connect

↓

Cursor

↓

Execute SQL

↓

Fetch Results

↓

Commit

↓

Close Resources
```

---

# Practice Exercises

## Exercise 1

Connect Python to MySQL.

---

## Exercise 2

Display MySQL Version.

---

## Exercise 3

Display all databases.

---

## Exercise 4

Display all tables.

---

## Exercise 5

Insert one student.

---

## Exercise 6

Display all students.

---

## Exercise 7

Update one student's marks.

---

## Exercise 8

Delete one student.

---

## Exercise 9

Handle database connection errors.

---

## Exercise 10

Create a reusable database connection function.

---

# Interview Questions

### 1. What is mysql-connector-python?

### 2. What is DB-API?

### 3. What is a Cursor?

### 4. Difference between fetchone(), fetchmany() and fetchall()?

### 5. Why do we use commit()?

### 6. What is rollback()?

### 7. Why should parameterized queries be used?

### 8. Why should connections be closed?

### 9. What causes "Access Denied" errors?

### 10. Explain the complete workflow of Python communicating with MySQL.

---

# Summary

Today we learned

✓ Python Database Programming

✓ DB-API

✓ MySQL Connector

✓ Connection Object

✓ Cursor Object

✓ execute()

✓ fetchone()

✓ fetchmany()

✓ fetchall()

✓ commit()

✓ rollback()

✓ Exception Handling

✓ Closing Connections

✓ Best Practices

---

# Coming Next (Day-37)

## Python + MySQL CRUD Application

- Menu-Driven Database Program
- Modular Programming
- Functions
- Complete CRUD Operations
- Search Records
- Report Generation
- Mini Student Management System
- Project Structure
- Code Organization
- Error Handling
