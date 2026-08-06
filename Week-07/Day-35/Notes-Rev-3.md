# Python Full Stack Foundation

# Week-07 – Day-35

# Part-3

# Database Relationships, Normalization & Database Design

## Using Modular Programming

---

# Objective

In Part-1, we created multiple tables.

In Part-2, we learned different types of JOINs.

In this session, we will understand how databases are designed using relationships and normalization.

---

# What is a Database Relationship?

A relationship connects two or more tables using a **Primary Key** and a **Foreign Key**.

Instead of storing duplicate information,

we connect tables together.

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

# Types of Relationships

```
Relationships

│

├── One-to-One

├── One-to-Many

└── Many-to-Many
```

---

# One-to-One Relationship

## What are we doing?

Each student is assigned one identity card.

One student has only one ID card.

One ID card belongs to only one student.

---

## Relationship

```
Student

1

↓

1

ID Card
```

---

## Tables

### Student

| Student_ID | Student |
|-----------:|---------|
|1|Alex|
|2|John|
|3|Mary|

---

### IDCard

| Card_ID | Student_ID |
|---------:|-----------:|
|101|1|
|102|2|
|103|3|

---

# Program-1

# Create ID Card Table

```python
from database import get_connection


def create_idcard_table():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    CREATE TABLE IF NOT EXISTS IDCard(

        card_id INT PRIMARY KEY,

        student_id INT UNIQUE,

        issue_date DATE,

        FOREIGN KEY(student_id)

        REFERENCES Student(student_id)

    )

    """)

    connection.commit()

    print("IDCard table created successfully.")

    cursor.close()

    connection.close()


def main():

    create_idcard_table()


if __name__ == "__main__":

    main()
```

---

# One-to-Many Relationship

## What are we doing?

One department contains many students.

Every student belongs to only one department.

---

## Relationship

```
Department

↓

Student

Student

Student
```

---

## Example

| Department | Students |
|------------|----------|
|CSE|Alex|
|CSE|David|
|CSE|Priya|

---

# Program-2

# Display Students with Department

```python
from database import get_connection


def department_students():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    SELECT

        Department.dept_name,

        Student.student_name

    FROM Department

    INNER JOIN Student

    ON Department.dept_id = Student.dept_id

    ORDER BY Department.dept_name

    """)

    rows = cursor.fetchall()

    print("Department\tStudent")
    print("----------------------------")

    for row in rows:
        print(row)

    cursor.close()

    connection.close()


def main():

    department_students()


if __name__ == "__main__":

    main()
```

---

## Output

```
('CSE', 'Alex')

('CSE', 'David')

('CSE', 'Priya')

('ECE', 'John')

('IT', 'Mary')
```

---

# Many-to-Many Relationship

## What are we doing?

Students can study many courses.

A course can have many students.

---

## Relationship

```
Student

↓

Enrollment

↓

Course
```

---

## Example

Alex

↓

Python

↓

SQL

John

↓

Java

Priya

↓

Python

↓

Java

---

# Program-3

# Display Student and Course

```python
from database import get_connection


def student_course():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    SELECT

        Student.student_name,

        Course.course_name

    FROM Student

    INNER JOIN Enrollment

    ON Student.student_id = Enrollment.student_id

    INNER JOIN Course

    ON Enrollment.course_id = Course.course_id

    ORDER BY Student.student_name

    """)

    rows = cursor.fetchall()

    print("Student\tCourse")
    print("------------------------")

    for row in rows:
        print(row)

    cursor.close()

    connection.close()


def main():

    student_course()


if __name__ == "__main__":

    main()
```

---

## Output

```
('Alex', 'Python')

('Alex', 'SQL')

('John', 'Java')

('Mary', 'Python')

('David', 'Machine Learning')

('Priya', 'Python')

('Priya', 'Java')
```

---

# Referential Integrity

## What are we doing?

Checking whether every Foreign Key exists in the referenced table.

---

## Why?

Foreign Keys prevent invalid records.

---

## Example

Department

```
1

2

3
```

Student

```
Dept_ID = 10
```

Result

```
Error

Foreign Key Constraint Failed
```

Because Department 10 does not exist.

---

# Database Normalization

## What is Normalization?

Normalization organizes data into multiple tables.

It removes duplicate data.

It improves consistency.

---

# First Normal Form (1NF)

## Rule

Every column must contain only one value.

---

### Incorrect

| Student | Courses |
|----------|---------|
|Alex|Python, SQL|

---

### Correct

| Student | Course |
|----------|--------|
|Alex|Python|
|Alex|SQL|

---

# Second Normal Form (2NF)

## Rule

Remove partial dependency.

Student information and Course information should be stored separately.

---

### Correct Design

```
Student

↓

Enrollment

↓

Course
```

---

# Third Normal Form (3NF)

## Rule

Remove transitive dependency.

Department information should not be repeated in the Student table.

---

### Bad Design

| Student | Department | HOD |
|----------|------------|-----|
|Alex|CSE|Ravi|
|John|ECE|Suresh|
|Mary|IT|Anil|

Department information is repeated.

---

### Better Design

```
Department

↓

Student
```

Department details are stored only once.

---

# Real World Database Designs

## College

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

## Hospital

```
Patient

↓

Appointment

↓

Doctor

↓

Medicine
```

---

## Banking

```
Customer

↓

Account

↓

Transaction
```

---

## E-Commerce

```
Customer

↓

Orders

↓

Order Items

↓

Products
```

---

# Program-4

# College Database Report

## What are we doing?

Generating a complete college report.

---

## Complete Code

```python
from database import get_connection


def college_report():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    SELECT

        Student.student_name,

        Department.dept_name,

        Course.course_name

    FROM Student

    INNER JOIN Department

        ON Student.dept_id = Department.dept_id

    INNER JOIN Enrollment

        ON Student.student_id = Enrollment.student_id

    INNER JOIN Course

        ON Enrollment.course_id = Course.course_id

    ORDER BY

        Department.dept_name,

        Student.student_name

    """)

    rows = cursor.fetchall()

    print("College Database Report")
    print("-------------------------------")

    for row in rows:
        print(row)

    cursor.close()

    connection.close()


def main():

    college_report()


if __name__ == "__main__":

    main()
```

---

## Output

```
('Alex', 'CSE', 'Python')

('Alex', 'CSE', 'SQL')

('David', 'CSE', 'Machine Learning')

('Priya', 'CSE', 'Python')

('Priya', 'CSE', 'Java')

('John', 'ECE', 'Java')

('Mary', 'IT', 'Python')
```

---

# Best Practices

- Always create a Primary Key.
- Use Foreign Keys to connect tables.
- Avoid duplicate data.
- Use meaningful table names.
- Normalize the database.
- Use JOINs instead of duplicate columns.
- Follow modular programming.
- Close database connections after every operation.

---

# Summary

In Part-3, we learned:

- One-to-One Relationship
- One-to-Many Relationship
- Many-to-Many Relationship
- Referential Integrity
- First Normal Form (1NF)
- Second Normal Form (2NF)
- Third Normal Form (3NF)
- Real-world Database Design
- College Database Report
- Best Practices for Database Design

After completing Parts 1, 2, and 3, you now have a complete understanding of **database design, relationships, normalization, and JOIN operations using MySQL with reusable modular Python code**.
