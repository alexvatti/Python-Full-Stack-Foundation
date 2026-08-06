# Python Full Stack Foundation

# SQLite vs MySQL

# Complete Comparison Guide

**Level:** Beginner → Intermediate

---

# Introduction

Both **SQLite** and **MySQL** are Relational Database Management Systems (RDBMS).

They store data in tables using SQL (Structured Query Language).

However, they are designed for different purposes.

---

# SQLite vs MySQL

| Feature | SQLite | MySQL |
|----------|---------|--------|
| Database Type | Embedded Database | Client-Server Database |
| Installation | No installation required | MySQL Server must be installed |
| Database Storage | Single `.db` file | Stored inside MySQL Server |
| Size | Very Small | Large |
| Performance | Good for small applications | Excellent for medium & large applications |
| Multi-user Support | Limited | Excellent |
| Networking | No | Yes |
| Security | Basic | Advanced |
| Concurrency | Limited | Supports many users |
| Transactions | Supported | Supported |
| License | Public Domain | GPL / Commercial |
| Python Module | sqlite3 | mysql.connector |

---

# Architecture

## SQLite

```
Python

↓

sqlite3

↓

college.db
```

Everything is stored in one database file.

---

## MySQL

```
Python

↓

mysql.connector

↓

MySQL Server

↓

college_db
```

The database is managed by a MySQL Server.

---

# Installation

## SQLite

No installation required.

Python already includes SQLite.

```python
import sqlite3
```

---

## MySQL

Install MySQL Server.

Install Python Connector.

```bash
pip install mysql-connector-python
```

Import

```python
import mysql.connector
```

---

# Database Creation

## SQLite

```python
import sqlite3

connection = sqlite3.connect("college.db")
```

Database file is created automatically.

---

## MySQL

```python
import mysql.connector

connection = mysql.connector.connect(

    host="localhost",

    user="root",

    password="root123"

)
```

Database must already exist.

---

# Creating Database

## SQLite

```
No CREATE DATABASE command.

Database file is created automatically.
```

---

## MySQL

```sql
CREATE DATABASE college_db;
```

---

# Selecting Database

## SQLite

```
Not Required
```

The database file itself is selected.

---

## MySQL

```sql
USE college_db;
```

Or

```python
database="college_db"
```

inside the connection.

---

# Python Connection

## SQLite

```python
import sqlite3

connection = sqlite3.connect("college.db")
```

---

## MySQL

```python
import mysql.connector

connection = mysql.connector.connect(

    host="localhost",

    user="root",

    password="root123",

    database="college_db"

)
```

---

# Cursor Object

Both databases use a Cursor.

SQLite

```python
cursor = connection.cursor()
```

MySQL

```python
cursor = connection.cursor()
```

Exactly the same.

---

# Execute SQL

SQLite

```python
cursor.execute(sql)
```

MySQL

```python
cursor.execute(sql)
```

Exactly the same.

---

# Commit

SQLite

```python
connection.commit()
```

MySQL

```python
connection.commit()
```

Exactly the same.

---

# Rollback

SQLite

```python
connection.rollback()
```

MySQL

```python
connection.rollback()
```

Exactly the same.

---

# Close Connection

SQLite

```python
connection.close()
```

MySQL

```python
connection.close()
```

Exactly the same.

---

# SQL Commands

| SQL Command | SQLite | MySQL |
|-------------|:------:|:------:|
| CREATE DATABASE | ❌ | ✅ |
| USE Database | ❌ | ✅ |
| CREATE TABLE | ✅ | ✅ |
| DROP TABLE | ✅ | ✅ |
| ALTER TABLE | ✅ | ✅ |
| INSERT | ✅ | ✅ |
| UPDATE | ✅ | ✅ |
| DELETE | ✅ | ✅ |
| SELECT | ✅ | ✅ |
| WHERE | ✅ | ✅ |
| ORDER BY | ✅ | ✅ |
| GROUP BY | ✅ | ✅ |
| HAVING | ✅ | ✅ |
| LIMIT | ✅ | ✅ |
| JOIN | ✅ | ✅ |
| VIEW | Limited | ✅ |
| INDEX | ✅ | ✅ |
| TRIGGER | ✅ | ✅ |

---

# Data Types

## SQLite Data Types

SQLite supports only a few storage classes.

| Data Type | Description |
|------------|-------------|
| NULL | Empty Value |
| INTEGER | Whole Numbers |
| REAL | Decimal Numbers |
| TEXT | Strings |
| BLOB | Binary Data |

SQLite is dynamically typed.

---

## MySQL Data Types

MySQL provides many data types.

### Numeric

- TINYINT
- SMALLINT
- MEDIUMINT
- INT
- BIGINT
- FLOAT
- DOUBLE
- DECIMAL

---

### Character

- CHAR
- VARCHAR
- TEXT
- MEDIUMTEXT
- LONGTEXT

---

### Date & Time

- DATE
- TIME
- DATETIME
- TIMESTAMP
- YEAR

---

### Binary

- BLOB
- LONGBLOB

---

### Boolean

```sql
BOOLEAN
```

Internally stored as

```
TINYINT(1)
```

---

# Auto Increment

SQLite

```sql
INTEGER PRIMARY KEY AUTOINCREMENT
```

---

MySQL

```sql
INT AUTO_INCREMENT PRIMARY KEY
```

---

# Placeholder Symbols

SQLite

```python
?
```

Example

```python
cursor.execute(

"SELECT * FROM Student WHERE id=?",

(id,)
)
```

---

MySQL

```python
%s
```

Example

```python
cursor.execute(

"SELECT * FROM Student WHERE id=%s",

(id,)
)
```

---

# Aggregate Functions

Both support

- COUNT()
- SUM()
- AVG()
- MIN()
- MAX()

Example

```sql
SELECT COUNT(*) FROM Student;
```

---

# String Functions

| Function | SQLite | MySQL |
|----------|:------:|:------:|
| UPPER() | ✅ | ✅ |
| LOWER() | ✅ | ✅ |
| LENGTH() | ✅ | ✅ |
| TRIM() | ✅ | ✅ |
| REPLACE() | ✅ | ✅ |
| SUBSTRING() | ✅ | ✅ |
| CONCAT() | ❌ | ✅ |
| LEFT() | ❌ | ✅ |
| RIGHT() | ❌ | ✅ |

---

# Numeric Functions

| Function | SQLite | MySQL |
|----------|:------:|:------:|
| ROUND() | ✅ | ✅ |
| ABS() | ✅ | ✅ |
| CEIL() | Limited | ✅ |
| FLOOR() | Limited | ✅ |
| POWER() | Limited | ✅ |
| SQRT() | Limited | ✅ |
| MOD() | ✅ | ✅ |

---

# Date Functions

## SQLite

- DATE()
- TIME()
- DATETIME()
- JULIANDAY()
- STRFTIME()

---

## MySQL

- CURDATE()
- CURTIME()
- NOW()
- YEAR()
- MONTH()
- DAY()
- DATE_ADD()
- DATE_SUB()
- DATEDIFF()

---

# Constraints

| Constraint | SQLite | MySQL |
|------------|:------:|:------:|
| PRIMARY KEY | ✅ | ✅ |
| FOREIGN KEY | ✅ | ✅ |
| UNIQUE | ✅ | ✅ |
| NOT NULL | ✅ | ✅ |
| CHECK | ✅ | ✅ |
| DEFAULT | ✅ | ✅ |

---

# Joins

Both support

- INNER JOIN
- LEFT JOIN
- CROSS JOIN
- SELF JOIN

MySQL additionally supports

- RIGHT JOIN

(SQLite typically requires rewriting RIGHT JOIN as LEFT JOIN.)

---

# Python Modules

SQLite

```python
import sqlite3
```

---

MySQL

```python
import mysql.connector
```

---

# Advantages of SQLite

- No installation required
- Lightweight
- Fast for small applications
- Easy to learn
- Single database file
- Portable
- Excellent for beginners

---

# Disadvantages of SQLite

- Limited concurrent users
- Not suitable for large enterprise systems
- Fewer built-in functions
- Limited security

---

# Advantages of MySQL

- High Performance
- Multi-user support
- Client-Server Architecture
- Better Security
- Large Database Support
- Excellent Transaction Support
- Enterprise Ready
- Rich SQL Functions

---

# Disadvantages of MySQL

- Requires installation
- Needs server configuration
- Slightly more complex for beginners
- Requires user management

---

# When Should You Use SQLite?

- Learning SQL
- Python Projects
- Desktop Applications
- Small Business Applications
- Embedded Systems
- Mobile Applications
- Local Data Storage

---

# When Should You Use MySQL?

- Web Applications
- Banking Systems
- Hospital Management
- College Management
- E-Commerce
- ERP Applications
- CRM Systems
- Enterprise Applications

---

# Summary

| Feature | SQLite | MySQL |
|----------|---------|--------|
| Installation | Not Required | Required |
| Database | File Based | Server Based |
| Speed | Fast (Small Projects) | Fast (Large Projects) |
| Multi-user | No | Yes |
| Security | Basic | Advanced |
| Networking | No | Yes |
| Python Module | sqlite3 | mysql.connector |
| Best For | Learning & Small Apps | Production Applications |

---

# Key Takeaways

- SQLite is simple, lightweight, and ideal for learning and small applications.
- MySQL is a powerful client-server database designed for multi-user and enterprise applications.
- Most SQL commands (`SELECT`, `INSERT`, `UPDATE`, `DELETE`, `JOIN`, `GROUP BY`, etc.) are the same in both databases.
- The main differences are in **installation, architecture, connection method, data types, placeholders (`?` vs `%s`), and advanced built-in functions.**
