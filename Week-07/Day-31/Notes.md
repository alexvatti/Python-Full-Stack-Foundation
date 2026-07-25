# Python Full Stack Foundation

# Week-07 – Day-31

# MySQL Database

# Introduction to MySQL, Installation & Database Server

**Level:** Beginner → Intermediate

**Duration:** 2–3 Hours

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Client-Server Databases
- Understand MySQL Architecture
- Differentiate SQLite and MySQL
- Install MySQL Community Server
- Install MySQL Workbench
- Connect to the MySQL Server
- Understand localhost
- Understand Port Numbers
- Create Your First MySQL Database
- Execute Basic SQL Commands
- Understand the MySQL Environment

---

# Agenda

1. Introduction
2. Why MySQL?
3. SQLite vs MySQL
4. Client-Server Architecture
5. MySQL Components
6. Installing MySQL
7. MySQL Workbench
8. Connecting to Server
9. Basic SQL Commands
10. Creating First Database

---

# Recap

Previous Week

✓ SQLite

✓ CREATE TABLE

✓ CRUD Operations

✓ Aggregate Functions

✓ Relationships

✓ Joins

Today

We move from

Serverless Database

↓

to

Client-Server Database

---

# Why Learn MySQL?

SQLite is excellent for

- Learning SQL
- Desktop Applications
- Small Projects

But

Large companies use

- MySQL
- PostgreSQL
- Oracle
- SQL Server

Therefore,

learning MySQL is an important next step.

---

# What is MySQL?

## Definition

MySQL is an open-source Relational Database Management System (RDBMS) that stores data on a dedicated database server.

Applications connect to the server to store and retrieve information.

---

# Real World Applications

MySQL is used in

- Banking Systems
- E-Commerce Websites
- Hospital Management
- College Management
- ERP Software
- HR Applications
- Inventory Systems
- Social Media Platforms

---

# Popular Companies Using MySQL

- Facebook (historically for many services)
- YouTube
- GitHub
- WordPress
- Drupal
- Joomla

---

# Why Companies Prefer MySQL?

✓ Fast

✓ Reliable

✓ Secure

✓ Multi-user Support

✓ Supports Large Databases

✓ Cross Platform

✓ Open Source

✓ High Performance

---

# SQLite vs MySQL

| SQLite | MySQL |
|----------|---------|
| Embedded Database | Client-Server Database |
| No Server | Dedicated Server |
| Single File | Database Folder |
| Built into Python | Separate Installation |
| Lightweight | Enterprise Ready |
| One User / Few Users | Thousands of Users |
| Local File | Network Accessible |

---

# Architecture Comparison

SQLite

```
Python Program

↓

SQLite Library

↓

college.db
```

---

MySQL

```
Python Program

↓

MySQL Connector

↓

MySQL Server

↓

Database
```

---

# What is a Database Server?

## Definition

A Database Server is software that stores databases and responds to requests from multiple users simultaneously.

---

# Real World Example

Imagine a Restaurant.

```
Customer

↓

Waiter

↓

Kitchen
```

Customer

↓

Application

Waiter

↓

MySQL Connector

Kitchen

↓

MySQL Server

---

# Client-Server Architecture

```
Client

↓

Network

↓

Database Server

↓

Database
```

---

# Real Example

```
Python Application

↓

MySQL Connector

↓

localhost

↓

MySQL Server

↓

College Database
```

---

# What is localhost?

## Definition

localhost refers to your own computer.

IP Address

```
127.0.0.1
```

When connecting locally,

the client communicates with the MySQL server running on the same machine.

---

# Default MySQL Port

```
3306
```

Port

A communication endpoint.

Example

```
localhost:3306
```

---

# What is a Port?

Think of a building.

```
Building

↓

Many Rooms

↓

Each Room

↓

Port
```

Different services use different ports.

Example

| Service | Port |
|----------|------|
| HTTP | 80 |
| HTTPS | 443 |
| MySQL | 3306 |
| PostgreSQL | 5432 |

---

# MySQL Components

```
MySQL

│

├── Server

├── Workbench

├── Command Line Client

├── Connectors

└── Databases
```

---

# MySQL Server

Responsible for

- Storing Databases
- Processing SQL
- User Authentication
- Backup
- Security

---

# MySQL Workbench

Workbench is a graphical interface used to

- Create Databases
- Create Tables
- Execute SQL
- View Data
- Design ER Diagrams
- Export Databases
- Import Databases

---

# Command Line Client

Allows execution of SQL commands from the terminal.

Example

```
mysql -u root -p
```

---

# Connectors

Programming languages communicate using connectors.

Examples

Python

↓

mysql-connector-python

Java

↓

JDBC

C#

↓

MySQL Connector/NET

PHP

↓

mysqli

---

# Installation

Download

```
MySQL Community Server
```

Install

↓

Server

↓

Workbench

↓

Command Line Client

---

# During Installation

Remember

Root Password

Example

```
Root User

↓

root

Password

↓

********
```

Store it safely.

---

# First Login

Open

MySQL Workbench

Choose

```
Local Instance MySQL80
```

Enter

```
Password
```

Connected successfully.

---

# MySQL Workbench Interface

```
Navigator

↓

Schemas

↓

SQL Editor

↓

Output Window
```

---

# SQL Editor

This is where SQL commands are written.

Example

```sql
SHOW DATABASES;
```

---

# First SQL Command

```sql
SELECT VERSION();
```

Output

```
8.x.x
```

Displays installed MySQL version.

---

# Show Databases

```sql
SHOW DATABASES;
```

Example Output

```
information_schema

mysql

performance_schema

sys
```

---

# System Databases

| Database | Purpose |
|------------|----------|
| mysql | User Accounts |
| information_schema | Metadata |
| performance_schema | Performance Monitoring |
| sys | Reports |

Do not modify these databases.

---

# Create Database

```sql
CREATE DATABASE college_db;
```

Output

```
Database Created
```

---

# Show Databases Again

```sql
SHOW DATABASES;
```

Output

```
college_db
```

---

# Select Database

```sql
USE college_db;
```

Output

```
Database changed
```

---

# Verify Current Database

```sql
SELECT DATABASE();
```

Output

```
college_db
```

---

# Show Tables

```sql
SHOW TABLES;
```

Initially

```
Empty Set
```

No tables exist yet.

---

# Delete Database

```sql
DROP DATABASE college_db;
```

Deletes the database permanently.

---

# Recreate Database

```sql
CREATE DATABASE college_db;

USE college_db;
```

Ready for table creation.

---

# MySQL Folder Structure

```
MySQL Server

│

├── Database

│      ├── Tables

│      ├── Indexes

│      └── Data

└── Users
```

---

# SQLite vs MySQL Workflow

SQLite

```
Python

↓

college.db
```

---

MySQL

```
Python

↓

Connector

↓

Server

↓

Database
```

---

# Advantages of MySQL

✓ Enterprise Ready

✓ High Speed

✓ Multi-user

✓ Secure

✓ Scalable

✓ Backup Support

✓ User Management

✓ Network Access

---

# Limitations

- Installation Required

- Server Must Be Running

- Slightly More Complex

- Requires Administration

---

# Best Practices

✓ Use meaningful database names.

✓ Never use the root account for production applications.

✓ Keep strong passwords.

✓ Create one database per project.

✓ Backup databases regularly.

---

# Common Mistakes

❌ Forgetting to start MySQL Server.

❌ Wrong password.

❌ Wrong port number.

❌ Forgetting

```sql
USE database_name;
```

before creating tables.

---

# Complete Workflow

```
Install MySQL

↓

Start MySQL Server

↓

Open Workbench

↓

Connect

↓

SHOW DATABASES

↓

CREATE DATABASE

↓

USE DATABASE

↓

SHOW TABLES
```

---

# Summary

Today we learned

✓ Introduction to MySQL

✓ SQLite vs MySQL

✓ Client-Server Architecture

✓ Database Server

✓ localhost

✓ Port 3306

✓ MySQL Components

✓ MySQL Workbench

✓ SQL Editor

✓ SHOW DATABASES

✓ CREATE DATABASE

✓ USE

✓ SHOW TABLES

✓ DROP DATABASE

---

# Software Used

- MySQL Community Server
- MySQL Workbench
- Command Line Client

---

# Coming Next (Day-32)

- CREATE TABLE in MySQL
- MySQL Data Types
- PRIMARY KEY
- AUTO_INCREMENT
- Constraints
- ALTER TABLE
- DESCRIBE TABLE
- SHOW CREATE TABLE
- Creating Student, Employee, Product and Department Tables
