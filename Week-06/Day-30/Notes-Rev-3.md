# Python Full Stack Foundation

# Week-06 – Day-30

# Part-3

# Program-9

# Many-to-Many Relationship

## What does it do?

This program creates a **Many-to-Many Relationship** between Students and Courses.

One student can enroll in many courses.

One course can have many students.

This relationship is implemented using an **Enrollment** table.

---

## Why do we use Many-to-Many?

Example

```
Alex

↓

Python

↓

SQL

↓

Java
```

Another Student

```
John

↓

Python

↓

HTML
```

Python course is attended by many students.

One student also learns many courses.

---

## Advantages

- Eliminates duplicate data
- Flexible database design
- Easy to add new courses
- Easy to generate reports
- Used in almost every ERP application

---

## Database Design

```
Student

↓

Enrollment

↓

Course
```

---

## We Want

- Create Student table
- Create Course table
- Create Enrollment table
- Display Student Name and Course Name

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("PRAGMA foreign_keys = ON")

cursor.execute("DROP TABLE IF EXISTS Enrollment")
cursor.execute("DROP TABLE IF EXISTS Student")
cursor.execute("DROP TABLE IF EXISTS Course")

cursor.execute("""
CREATE TABLE Student(
    student_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT
)
""")

cursor.execute("""
CREATE TABLE Course(
    course_id INTEGER PRIMARY KEY AUTOINCREMENT,
    course_name TEXT
)
""")

cursor.execute("""
CREATE TABLE Enrollment(
    enrollment_id INTEGER PRIMARY KEY AUTOINCREMENT,
    student_id INTEGER,
    course_id INTEGER,
    FOREIGN KEY(student_id) REFERENCES Student(student_id),
    FOREIGN KEY(course_id) REFERENCES Course(course_id)
)
""")

students = [
    ("Alex",),
    ("John",),
    ("Priya",)
]

courses = [
    ("Python",),
    ("SQL",),
    ("Java",)
]

enrollments = [
    (1,1),
    (1,2),
    (2,1),
    (2,3),
    (3,2)
]

cursor.executemany("INSERT INTO Student(name) VALUES(?)",students)
cursor.executemany("INSERT INTO Course(course_name) VALUES(?)",courses)
cursor.executemany("INSERT INTO Enrollment(student_id,course_id) VALUES(?,?)",enrollments)

connection.commit()

cursor.execute("""
SELECT
Student.name,
Course.course_name
FROM Enrollment
INNER JOIN Student
ON Enrollment.student_id = Student.student_id
INNER JOIN Course
ON Enrollment.course_id = Course.course_id
""")

rows = cursor.fetchall()

print("Student\tCourse")
print("-------------------------")

for row in rows:
    print(row[0],"\t",row[1])

connection.close()
```

---

## Output

```
Student     Course
-------------------------
Alex        Python
Alex        SQL
John        Python
John        Java
Priya       SQL
```

---

## Industry Usage

- College Management System
- Online Learning Platforms
- Library Management
- Employee Training
- Hospital Appointments

---

# Program-10

# INNER JOIN

## What does it do?

Displays only matching records from two related tables.

---

## Why do we use INNER JOIN?

Student table contains

```
Department ID
```

Department table contains

```
Department Name
```

INNER JOIN combines both tables into one report.

---

## Advantages

- Combines related tables
- Easy report generation
- Removes duplicate information
- Fast data retrieval

---

## We Want

Display

- Student ID
- Student Name
- Department Name

---

## Complete Code

```python
import sqlite3

connection = sqlite3.connect("college.db")

cursor = connection.cursor()

cursor.execute("PRAGMA foreign_keys = ON")

cursor.execute("DROP TABLE IF EXISTS Student")
cursor.execute("DROP TABLE IF EXISTS Department")

cursor.execute("""
CREATE TABLE Department(
dept_id INTEGER PRIMARY KEY,
dept_name TEXT
)
""")

cursor.execute("""
CREATE TABLE Student(
student_id INTEGER PRIMARY KEY,
name TEXT,
dept_id INTEGER,
FOREIGN KEY(dept_id)
REFERENCES Department(dept_id)
)
""")

cursor.executemany(
"INSERT INTO Department VALUES(?,?)",
[
(1,"CSE"),
(2,"ECE"),
(3,"IT")
]
)

cursor.executemany(
"INSERT INTO Student VALUES(?,?,?)",
[
(1,"Alex",1),
(2,"John",2),
(3,"Priya",3),
(4,"Neha",1)
]
)

connection.commit()

cursor.execute("""
SELECT
Student.student_id,
Student.name,
Department.dept_name
FROM Student
INNER JOIN Department
ON Student.dept_id=Department.dept_id
""")

rows=cursor.fetchall()

print("ID\tName\tDepartment")
print("---------------------------")

for row in rows:
    print(row[0],"\t",row[1],"\t",row[2])

connection.close()
```

---

## Output

```
ID  Name    Department
---------------------------
1   Alex    CSE
2   John    ECE
3   Priya   IT
4   Neha    CSE
```

---

## Industry Usage

- Employee & Department
- Customer & Orders
- Product & Category
- Doctor & Hospital

---

# Program-11

# LEFT JOIN

## What does it do?

Displays all records from the **left table** and matching records from the right table.

If no matching record exists,

SQLite displays

```
NULL
```

---

## Why do we use LEFT JOIN?

Sometimes,

we want to display all students,

even if they are not assigned to any department.

---

## Advantages

- Complete reports
- Finds missing relationships
- Useful for auditing
- Better data analysis

---

## We Want

Display every student along with the department name.

---

## Complete Code

```python
import sqlite3

connection=sqlite3.connect("college.db")

cursor=connection.cursor()

cursor.execute("""
CREATE TABLE Department(
dept_id INTEGER PRIMARY KEY,
dept_name TEXT
)
""")

cursor.execute("""
CREATE TABLE Student(
student_id INTEGER PRIMARY KEY,
name TEXT,
dept_id INTEGER
)
""")

cursor.executemany(
"INSERT INTO Department VALUES(?,?)",
[
(1,"CSE"),
(2,"ECE")
]
)

cursor.executemany(
"INSERT INTO Student VALUES(?,?,?)",
[
(1,"Alex",1),
(2,"John",2),
(3,"Priya",None),
(4,"Neha",1)
]
)

connection.commit()

cursor.execute("""
SELECT
Student.name,
Department.dept_name
FROM Student
LEFT JOIN Department
ON Student.dept_id=Department.dept_id
""")

rows=cursor.fetchall()

print("Student\tDepartment")
print("-----------------------")

for row in rows:
    print(row)

connection.close()
```

---

## Output

```
Student     Department
-----------------------
('Alex', 'CSE')
('John', 'ECE')
('Priya', None)
('Neha', 'CSE')
```

---

## Industry Usage

- Students without Department
- Employees without Project
- Customers without Orders
- Products without Category

---

# Program-12

# Complete College Database Report

## What does it do?

Creates a complete College Database and generates a report using multiple tables.

---

## Why do we use it?

Real-world applications never store everything in one table.

Instead,

they divide data into multiple related tables.

---

## Advantages

- Real-world database design
- Demonstrates relationships
- Better performance
- Easy maintenance
- Easy reporting

---

## Database Structure

```
Department

↓

Student

↓

Enrollment

↓

Course
```

---

## We Want

Display

- Student Name
- Department
- Course Name

---

## Complete Code

```python
import sqlite3

connection=sqlite3.connect("college.db")

cursor=connection.cursor()

cursor.execute("PRAGMA foreign_keys = ON")

cursor.executescript("""

DROP TABLE IF EXISTS Enrollment;
DROP TABLE IF EXISTS Student;
DROP TABLE IF EXISTS Course;
DROP TABLE IF EXISTS Department;

CREATE TABLE Department(
dept_id INTEGER PRIMARY KEY,
dept_name TEXT
);

CREATE TABLE Student(
student_id INTEGER PRIMARY KEY,
name TEXT,
dept_id INTEGER,
FOREIGN KEY(dept_id)
REFERENCES Department(dept_id)
);

CREATE TABLE Course(
course_id INTEGER PRIMARY KEY,
course_name TEXT
);

CREATE TABLE Enrollment(
student_id INTEGER,
course_id INTEGER,
FOREIGN KEY(student_id)
REFERENCES Student(student_id),
FOREIGN KEY(course_id)
REFERENCES Course(course_id)
);

""")

cursor.executemany(
"INSERT INTO Department VALUES(?,?)",
[
(1,"CSE"),
(2,"ECE")
]
)

cursor.executemany(
"INSERT INTO Student VALUES(?,?,?)",
[
(1,"Alex",1),
(2,"John",2),
(3,"Priya",1)
]
)

cursor.executemany(
"INSERT INTO Course VALUES(?,?)",
[
(1,"Python"),
(2,"SQL"),
(3,"Java")
]
)

cursor.executemany(
"INSERT INTO Enrollment VALUES(?,?)",
[
(1,1),
(1,2),
(2,3),
(3,1),
(3,3)
]
)

connection.commit()

cursor.execute("""
SELECT
Student.name,
Department.dept_name,
Course.course_name
FROM Enrollment
INNER JOIN Student
ON Enrollment.student_id=Student.student_id
INNER JOIN Department
ON Student.dept_id=Department.dept_id
INNER JOIN Course
ON Enrollment.course_id=Course.course_id
ORDER BY Student.name
""")

rows=cursor.fetchall()

print("Student\tDepartment\tCourse")
print("------------------------------------------")

for row in rows:
    print(row[0],"\t",row[1],"\t\t",row[2])

connection.close()
```

---

## Output

```
Student     Department      Course
------------------------------------------
Alex        CSE             Python
Alex        CSE             SQL
John        ECE             Java
Priya       CSE             Python
Priya       CSE             Java
```

---

# Summary

In Part-3, we learned:

✅ Many-to-Many Relationship

✅ INNER JOIN

✅ LEFT JOIN

✅ Complete College Database Project

---

# Congratulations! 🎉

You have now completed the complete **SQLite Programming Module**.

### Topics Covered

- ✅ SQLite Basics
- ✅ Database Connection
- ✅ CREATE TABLE
- ✅ Data Types
- ✅ Constraints
- ✅ CRUD Operations
- ✅ SELECT Queries
- ✅ Aggregate Functions
- ✅ GROUP BY
- ✅ HAVING
- ✅ Relationships
- ✅ JOIN Operations
- ✅ Mini Database Project

You are now ready to move on to **Week-07: MySQL Database Programming**.
