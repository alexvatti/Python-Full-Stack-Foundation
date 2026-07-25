# Python Full Stack Foundation

# Week-08 – Day-37

# Python + MySQL Integration

# Building a Complete CRUD Application (Menu-Driven Student Management System)

**Level:** Beginner → Intermediate

**Duration:** 3 Hours

---

# Learning Objectives

By the end of this session, you will be able to:

- Build a Complete CRUD Application
- Design a Menu-Driven Program
- Organize Python Code using Functions
- Perform CRUD Operations from Python
- Search Records
- Display Reports
- Handle Exceptions
- Validate User Input
- Write Reusable Database Functions
- Understand Project Structure

---

# Agenda

1. Project Overview
2. Application Flow
3. Project Structure
4. Database Connection
5. CRUD Functions
6. Search Function
7. Menu System
8. Exception Handling
9. Reports
10. Best Practices

---

# Recap

Previous Session

✓ Python MySQL Connector

✓ Database Connection

✓ Cursor

✓ execute()

✓ fetch()

✓ commit()

✓ rollback()

Today

We will build a complete database application.

---

# Mini Project

## Student Management System

Features

- Add Student
- View Students
- Search Student
- Update Student
- Delete Student
- Exit

---

# Application Flow

```
Start

↓

Connect Database

↓

Display Menu

↓

User Choice

↓

Perform Operation

↓

Return to Menu

↓

Exit
```

---

# Project Structure

```
StudentManagement/

│

├── database.py

├── student.py

├── menu.py

├── main.py

└── config.py
```

---

# Database Design

Student Table

```sql
CREATE TABLE Student(

student_id INT AUTO_INCREMENT PRIMARY KEY,

name VARCHAR(100),

department VARCHAR(50),

marks DECIMAL(5,2)

);
```

---

# Step 1

Import Library

```python
import mysql.connector
```

---

# Step 2

Database Connection Function

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

---

# Why Functions?

Without Functions

```
Repeated Code
```

With Functions

```
Reusable Code
```

---

# Function Layout

```
main()

↓

add_student()

↓

view_students()

↓

update_student()

↓

delete_student()

↓

search_student()
```

---

# Add Student

```python
def add_student():

    connection=get_connection()

    cursor=connection.cursor()

    name=input("Name : ")

    department=input("Department : ")

    marks=float(input("Marks : "))

    sql="""

    INSERT INTO Student

    (name,department,marks)

    VALUES(%s,%s,%s)

    """

    cursor.execute(sql,(name,department,marks))

    connection.commit()

    print("Student Added")

    cursor.close()

    connection.close()
```

---

# View Students

```python
def view_students():

    connection=get_connection()

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

# Search Student by ID

```python
def search_student():

    connection=get_connection()

    cursor=connection.cursor()

    sid=int(input("Student ID : "))

    cursor.execute(

        "SELECT * FROM Student WHERE student_id=%s",

        (sid,)

    )

    row=cursor.fetchone()

    print(row)

    cursor.close()

    connection.close()
```

---

# Search Student by Name

```python
cursor.execute(

"SELECT * FROM Student

WHERE name=%s",

(name,)

)
```

---

# Update Student

```python
def update_student():

    connection=get_connection()

    cursor=connection.cursor()

    sid=int(input("Student ID : "))

    marks=float(input("New Marks : "))

    cursor.execute(

    """

    UPDATE Student

    SET marks=%s

    WHERE student_id=%s

    """,

    (marks,sid)

    )

    connection.commit()

    print("Updated")

    cursor.close()

    connection.close()
```

---

# Delete Student

```python
def delete_student():

    connection=get_connection()

    cursor=connection.cursor()

    sid=int(input("Student ID : "))

    cursor.execute(

    """

    DELETE FROM Student

    WHERE student_id=%s

    """,

    (sid,)

    )

    connection.commit()

    print("Deleted")

    cursor.close()

    connection.close()
```

---

# Count Students

```python
def total_students():

    connection=get_connection()

    cursor=connection.cursor()

    cursor.execute(

    "SELECT COUNT(*) FROM Student"

    )

    total=cursor.fetchone()

    print(total)

    cursor.close()

    connection.close()
```

---

# Highest Marks

```python
cursor.execute(

"""

SELECT

MAX(marks)

FROM Student

"""

)

print(cursor.fetchone())
```

---

# Student Report

```python
cursor.execute(

"""

SELECT

department,

COUNT(*),

AVG(marks)

FROM Student

GROUP BY department

"""

)

rows=cursor.fetchall()

for row in rows:

    print(row)
```

---

# Menu Design

```
**********************

Student Management

**********************

1 Add Student

2 View Students

3 Search Student

4 Update Student

5 Delete Student

6 Reports

7 Exit

**********************
```

---

# Menu Function

```python
def menu():

    while True:

        print()

        print("1 Add Student")

        print("2 View Students")

        print("3 Search Student")

        print("4 Update Student")

        print("5 Delete Student")

        print("6 Reports")

        print("7 Exit")

        choice=int(input("Choice : "))

        if choice==1:

            add_student()

        elif choice==2:

            view_students()

        elif choice==3:

            search_student()

        elif choice==4:

            update_student()

        elif choice==5:

            delete_student()

        elif choice==6:

            total_students()

        elif choice==7:

            print("Thank You")

            break

        else:

            print("Invalid Choice")
```

---

# Main Function

```python
def main():

    menu()

main()
```

---

# Exception Handling

```python
try:

    connection=get_connection()

except Exception as e:

    print(e)
```

---

# Better Exception Handling

```python
try:

    add_student()

except ValueError:

    print("Enter Proper Number")

except Exception as e:

    print(e)
```

---

# Input Validation

Wrong

```python
marks=float(input())
```

User enters

```
abc
```

Program crashes.

---

Correct

```python
while True:

    try:

        marks=float(input("Marks : "))

        break

    except:

        print("Invalid Marks")
```

---

# Search Using LIKE

```python
cursor.execute(

"""

SELECT *

FROM Student

WHERE name LIKE %s

""",

("%A%",)

)
```

---

# Display Students

```
ID

Name

Department

Marks
```

Instead of

```
(1,'Alex','CSE',91)
```

---

Better Output

```python
for row in rows:

    print(

    row[0],

    row[1],

    row[2],

    row[3]

    )
```

---

# Modular Programming

```
database.py

↓

Connection

student.py

↓

CRUD Functions

menu.py

↓

Menu

main.py

↓

Execution
```

---

# Program Workflow

```
Start

↓

Connection

↓

Menu

↓

CRUD

↓

Commit

↓

Display Result

↓

Repeat

↓

Exit
```

---

# Common Errors

## MySQL Server Not Running

```
Can't Connect
```

---

## Wrong Password

```
Access Denied
```

---

## Wrong SQL

```
Programming Error
```

---

## Invalid Input

```
ValueError
```

---

# Best Practices

✓ Create reusable functions.

✓ Close connections.

✓ Validate user input.

✓ Use parameterized queries.

✓ Commit only when required.

✓ Display user-friendly messages.

✓ Handle exceptions.

✓ Separate files logically.

---

# Real World Improvements

Future enhancements

- Login Screen
- Password Protection
- Search by Name
- Department Filter
- Export CSV
- Import Excel
- GUI using Tkinter
- Web Version using Flask
- REST API
- Role-Based Access

---

# Mini Project Architecture

```
Student Management

│

├── Login

├── Add Student

├── View Students

├── Search

├── Update

├── Delete

├── Reports

└── Exit
```

---

# Practice Exercises

## Exercise 1

Create a reusable database connection function.

---

## Exercise 2

Write a function to insert a student.

---

## Exercise 3

Display all students in tabular format.

---

## Exercise 4

Search student using ID.

---

## Exercise 5

Search student using Name.

---

## Exercise 6

Update marks.

---

## Exercise 7

Delete student.

---

## Exercise 8

Display total number of students.

---

## Exercise 9

Generate department-wise report.

---

## Exercise 10

Build the complete Student Management System using functions and a menu.

---

# Interview Questions

### 1. Why should database code be placed inside functions?

### 2. Why is modular programming useful?

### 3. Why should parameterized queries be used?

### 4. What is the purpose of commit()?

### 5. What happens if connection.close() is not called?

### 6. Why do we use a while loop for menus?

### 7. How do you handle invalid user input?

### 8. How would you organize a medium-sized Python project?

### 9. How would you search records efficiently?

### 10. What improvements would you make to this project?

---

# Summary

Today we learned

✓ Menu-Driven Programming

✓ CRUD Functions

✓ Search Operations

✓ Reports

✓ Modular Programming

✓ Input Validation

✓ Exception Handling

✓ Reusable Database Functions

✓ Student Management System

✓ Project Structure

---

# Coming Next (Week-09 – Day-38)

## Python + MySQL Advanced Programming

- Transactions (COMMIT & ROLLBACK)
- Batch Insert (`executemany()`)
- Stored Procedures (Introduction)
- Pagination
- Configuration Files
- Logging
- Export to CSV
- Import from CSV
- Building a Professional Database Utility Module
- Final Python + MySQL Mini Project
