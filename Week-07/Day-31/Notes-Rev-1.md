# MySQL Database Setup Guide

## Python Full Stack Foundation

### Using FreeSQLDatabase.com

---

# Objective

In this document, you will learn how to:

- Create a free MySQL database
- Obtain database credentials
- Connect to the database
- Verify the connection
- Prepare the database for Python applications

---

# Step 1: Create a Free Account

Open the following website:

https://www.freesqldatabase.com/account/

Create your free account and verify your email address.

---

# Step 2: Login

After logging in, open your dashboard.

You will see information similar to:

```
Account Details

Account Number : 1707169

Available Databases : 0 of 1

Available Space : 5 MB
```

---

# Step 3: Database Details

Your dashboard displays something similar to:

| Field | Example |
|--------|---------|
| Host | sql12.freesqldatabase.com |
| Database Name | sql12834641 |
| Username | sql12834641 |
| Password | Check your Email |
| Status | Live |

Example

```
Host

sql12.freesqldatabase.com

Database

sql12834641

Username

sql12834641

Password

Check your Email
```

> **Important:** The database password is sent to your registered email address. Save it securely.

---

# Step 4: Save Your Credentials

Create a text file named:

```
database_info.txt
```

Save the following information:

```
Host

sql12.freesqldatabase.com

Database

sql12834641

Username

sql12834641

Password

****************
```

Never share this password publicly.

---

# Step 5: Install MySQL Connector

Open Command Prompt or Terminal.

Run:

```bash
pip install mysql-connector-python
```

Verify installation:

```bash
pip show mysql-connector-python
```

---

# Step 6: Test Internet Connection

Make sure your computer is connected to the Internet.

Since this is a cloud database,

an active Internet connection is required.

---

# Step 7: Create Project Folder

```
PythonFullStack

│

├── mysql_demo.py

├── config.py

└── database_info.txt
```

---

# Step 8: Create Configuration File

Create a file named

```
config.py
```

Example

```python
HOST = "sql12.freesqldatabase.com"

DATABASE = "sql12834641"

USERNAME = "sql12834641"

PASSWORD = "YOUR_PASSWORD"
```

Replace

```
YOUR_PASSWORD
```

with the password received by email.

---

# Step 9: Create Connection Program

Create

```
mysql_demo.py
```

```python
import mysql.connector

from config import HOST
from config import DATABASE
from config import USERNAME
from config import PASSWORD

connection = mysql.connector.connect(
    host=HOST,
    database=DATABASE,
    user=USERNAME,
    password=PASSWORD
)

if connection.is_connected():
    print("Connected Successfully")

connection.close()
```

---

# Step 10: Run the Program

Execute:

```bash
python mysql_demo.py
```

---

# Expected Output

```
Connected Successfully
```

---

# Common Errors

## Error 1

```
Access denied
```

### Reason

Incorrect username or password.

### Solution

Check the password received by email.

---

## Error 2

```
Unknown database
```

### Reason

Database name is incorrect.

### Solution

Copy the database name exactly from the dashboard.

---

## Error 3

```
Can't connect to MySQL server
```

### Reason

- Internet connection unavailable
- Incorrect host name
- Server temporarily unavailable

### Solution

Verify:

- Internet connection
- Host name
- Database status

---

## Error 4

```
ModuleNotFoundError

No module named mysql.connector
```

### Solution

Install the connector:

```bash
pip install mysql-connector-python
```

---

# Best Practices

- Never hardcode passwords in multiple files.
- Store credentials in a separate configuration file.
- Never upload passwords to GitHub.
- Keep your password private.
- Always close the database connection after use.

---

# Database Information Checklist

| Item | Status |
|------|:------:|
| Free Account Created | ☐ |
| Email Verified | ☐ |
| Database Created | ☐ |
| Host Name Saved | ☐ |
| Database Name Saved | ☐ |
| Username Saved | ☐ |
| Password Saved | ☐ |
| MySQL Connector Installed | ☐ |
| Connection Tested | ☐ |
| Successfully Connected | ☐ |

---

# Next Session

After successfully connecting to MySQL, you are ready to learn:

- Create Database
- Create Table
- Insert Records
- SELECT
- UPDATE
- DELETE
- CRUD Operations using Python and MySQL
