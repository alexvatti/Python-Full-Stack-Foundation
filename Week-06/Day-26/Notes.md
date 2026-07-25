# Python Full Stack Foundation

# Week-06 – Day-26

# Introduction to Databases & SQLite

**Level:** Beginner → Intermediate

**Duration:** 2-3 Hours

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Data and Information
- Understand Database concepts
- Explain DBMS
- Explain RDBMS
- Differentiate File System and Database
- Understand SQL
- Explain SQLite
- Connect Python with SQLite
- Create your first SQLite Database
- Execute your first SQL statement using Python

---

# Agenda

1. Data
2. Information
3. File System
4. Database
5. DBMS
6. RDBMS
7. SQL
8. SQLite
9. Python sqlite3 Module
10. Creating Database
11. Database Connection
12. First SQL Program

---

# What is Data?

## Definition

Data is a collection of raw facts and figures that have no meaning by themselves.

Examples

```
Alex

101

85

Hyderabad

50000
```

These values alone do not provide useful information.

---

# Examples of Data

Student Name

```
Alex
```

Age

```
22
```

Marks

```
95
```

Salary

```
55000
```

Product Price

```
1500
```

---

# What is Information?

## Definition

Information is processed and organized data that has meaning.

Example

```
Student Name : Alex

Roll Number : 101

Department : CSE

Marks : 95

Result : PASS
```

Now the data becomes useful.

---

# Data vs Information

| Data | Information |
|------|-------------|
| Raw Facts | Processed Data |
| No Meaning | Meaningful |
| Unorganized | Organized |
| Input | Output |

---

# Real World Example

Hospital

Raw Data

```
Patient ID

Age

Temperature

Blood Pressure
```

Information

```
Patient is suffering from Fever.

Medicine Required.
```

---

# Another Example

Bank

Raw Data

```
Deposit

Withdraw

Balance
```

Information

```
Current Balance : £8,500
```

---

# Traditional File System

Before databases, information was stored in files.

Example

```
students.txt

employees.txt

products.txt

customers.txt
```

---

# Example

Student.txt

```
101,Alex,95

102,John,88

103,Ravi,79
```

---

# Problems with File Systems

## 1 Data Duplication

Student details stored multiple times.

```
Student File

Library File

Exam File

Hostel File
```

Repeated information wastes storage.

---

## 2 Difficult Searching

Finding one student's information becomes slow.

---

## 3 No Security

Anyone can open and edit the file.

---

## 4 Data Inconsistency

One file

```
Alex
```

Another file

```
Alexander
```

Which one is correct?

---

## 5 Backup Problems

If the file is deleted,

the data is lost.

---

## 6 Multi-user Problem

Two users editing the same file simultaneously can overwrite each other's changes.

---

# Solution

Database

---

# What is a Database?

## Definition

A Database is an organized collection of related data stored electronically.

It allows users to

- Store Data
- Retrieve Data
- Update Data
- Delete Data

efficiently.

---

# Examples of Databases

- School Management System
- Hospital Management System
- Banking System
- Railway Reservation
- E-Commerce Website
- Library Management
- Employee Payroll
- Inventory System

---

# Database Representation

```
Database

│

├── Student Table

├── Employee Table

├── Product Table

└── Orders Table
```

---

# What is DBMS?

## Definition

DBMS stands for

**Database Management System**

A DBMS is software that allows users to create, store, retrieve and manage databases.

---

# Responsibilities of DBMS

- Store Data
- Retrieve Data
- Update Data
- Delete Data
- Backup Data
- Security
- User Management

---

# Examples of DBMS

- SQLite
- MySQL
- PostgreSQL
- Oracle Database
- Microsoft SQL Server
- MariaDB

---

# Advantages of DBMS

✓ Reduced Data Redundancy

✓ Better Security

✓ Faster Searching

✓ Data Integrity

✓ Backup and Recovery

✓ Multiple User Support

✓ Easy Maintenance

---

# Disadvantages of DBMS

- Initial Learning Curve
- Slightly More Complex than Files
- Requires Proper Design

---

# What is RDBMS?

## Definition

RDBMS stands for

**Relational Database Management System**

Data is stored in the form of tables.

Tables are related to each other using keys.

---

# Table Structure

```
Student

+------+--------+-------+

| ID   | Name   | Marks |

+------+--------+-------+

|101   | Alex   | 95    |

|102   | John   | 88    |

+------+--------+-------+
```

---

# Why "Relational"?

Student Table

↓

Student_ID

↓

Marks Table

↓

Library Table

↓

Fees Table

All are connected using relationships.

---

# DBMS vs RDBMS

| DBMS | RDBMS |
|------|--------|
| Data may not be relational | Data stored in related tables |
| Limited relationships | Strong relationships |
| Less scalable | Highly scalable |
| Small Applications | Enterprise Applications |

---

# Popular RDBMS

| Database | Open Source | Server Required |
|-----------|-------------|----------------|
| SQLite | Yes | No |
| MySQL | Yes | Yes |
| PostgreSQL | Yes | Yes |
| Oracle | No | Yes |
| SQL Server | No | Yes |

---

# What is SQL?

## Definition

SQL stands for

**Structured Query Language**

SQL is used to communicate with databases.

---

# SQL Can

- Create Databases
- Create Tables
- Insert Data
- Read Data
- Update Data
- Delete Data

---

# SQL Categories

```
SQL

│

├── DDL

├── DML

├── DQL

├── DCL

└── TCL
```

---

# DDL

Data Definition Language

Commands

```
CREATE

ALTER

DROP

TRUNCATE
```

Used for database structure.

---

# DML

Data Manipulation Language

Commands

```
INSERT

UPDATE

DELETE
```

Used to modify data.

---

# DQL

Data Query Language

Command

```
SELECT
```

Used to retrieve data.

---

# DCL

Data Control Language

Commands

```
GRANT

REVOKE
```

Used for permissions.

---

# TCL

Transaction Control Language

Commands

```
COMMIT

ROLLBACK

SAVEPOINT
```

Used for transaction management.

---

# What is SQLite?

## Definition

SQLite is a lightweight, serverless relational database that stores the entire database in a single file.

---

# Features of SQLite

✓ Built into Python

✓ Serverless

✓ Zero Configuration

✓ Cross Platform

✓ Lightweight

✓ Fast

✓ Portable

✓ Open Source

---

# Advantages of SQLite

- No Installation Required
- Easy to Learn
- Single File Database
- Perfect for Learning SQL
- Ideal for Desktop Applications
- Great for Small Projects

---

# Limitations of SQLite

- Not ideal for very high concurrent users
- Limited scalability compared to enterprise database servers
- Fewer administration features than MySQL or PostgreSQL

---

# Where SQLite is Used

- Android Applications
- Mobile Apps
- Desktop Software
- Web Browsers
- IoT Devices
- Embedded Systems
- Small Business Applications
- Python Projects

---

# SQLite vs MySQL

| SQLite | MySQL |
|----------|--------|
| Embedded Database | Client-Server Database |
| Single File | Separate Server |
| No Installation | Installation Required |
| Built into Python | External Connector Required |
| Best for Learning | Best for Production |

---

# Python sqlite3 Module

Python provides a built-in module named

```python
sqlite3
```

No installation is required.

Import it using

```python
import sqlite3
```

---

# Creating Your First Database

```python
import sqlite3

connection = sqlite3.connect("college.db")

connection.close()
```

Output

```
college.db file created
```

---

# Understanding the Code

```python
import sqlite3
```

Imports the SQLite module.

---

```python
sqlite3.connect("college.db")
```

Creates a database file if it does not exist.

If it already exists,

Python simply opens it.

---

```python
connection.close()
```

Closes the database connection.

Always close the connection after completing database operations.

---

# Database File

After running the program

```
Project Folder

│

├── main.py

└── college.db
```

The database is just a normal file.

---

# Complete Program

```python
import sqlite3

print("Connecting...")

connection = sqlite3.connect("college.db")

print("Database Connected Successfully")

connection.close()

print("Connection Closed")
```

Sample Output

```
Connecting...

Database Connected Successfully

Connection Closed
```

---

# Real-World Workflow

```
Python Program

↓

sqlite3 Module

↓

college.db

↓

Store Data
```

---

# Best Practices

✔ Always close database connections.

✔ Keep one database per project.

✔ Use meaningful database names.

✔ Store the database inside the project folder.

✔ Handle database errors using exception handling (covered later).

---

# Common Mistakes

❌ Forgetting to close the connection.

❌ Creating multiple unnecessary database files.

❌ Assuming SQLite requires a separate server.

❌ Confusing a database file with a Python file.

---

# Summary

Today we learned

✓ Data

✓ Information

✓ File System

✓ Database

✓ DBMS

✓ RDBMS

✓ SQL

✓ SQL Categories

✓ SQLite

✓ Advantages of SQLite

✓ Python sqlite3 Module

✓ Creating a Database

✓ Connecting and Closing a Database

---

# Coming Next (Day-27)

- Cursor Object
- SQL Statements
- CREATE TABLE
- SQLite Data Types
- execute()
- commit()
- Reading Database Schema
- Creating Student, Employee and Product Tables
