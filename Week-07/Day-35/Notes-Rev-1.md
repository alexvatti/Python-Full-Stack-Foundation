# Python Full Stack Foundation

# Week-07 – Day-35

# Part-1

# Database Relationships & Table Creation

## Using Modular Programming

---

# Objective

In the previous sessions, we learned CRUD operations and SQL functions.

In this session, we will learn how multiple tables are connected using **Primary Keys** and **Foreign Keys**.

Instead of storing everything in one table, we divide the data into multiple related tables.

All programs use the common reusable database connection.

```python
from database import get_connection
```

---

# College Database

We are going to build a simple College Database.

The database contains four tables.

```
College Database

│

├── Department

├── Student

├── Course

└── Enrollment
```

---

# Relationship

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

# Department Table

Stores department information.

| Dept_ID | Department |
|----------|------------|
|1|CSE|
|2|ECE|
|3|IT|

---

# Student Table

Stores student information.

| Student_ID | Name | Dept_ID |
|-----------:|------|---------|
|1|Alex|1|
|2|John|2|
|3|Mary|3|

---

# Course Table

Stores course details.

| Course_ID | Course |
|-----------:|---------|
|101|Python|
|102|Java|
|103|SQL|

---

# Enrollment Table

Stores which student enrolled in which course.

| Student_ID | Course_ID |
|-----------:|----------:|
|1|101|
|1|103|
|2|102|
|3|101|

---

# Program-1

# Create Department Table

## What are we doing?

Creating the Department table.

Each department will have a unique Department ID.

---

## Why?

Instead of storing department names repeatedly,

we store them only once.

---

## Complete Code

```python
from database import get_connection


def create_department_table():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    CREATE TABLE IF NOT EXISTS Department(

        dept_id INT AUTO_INCREMENT PRIMARY KEY,

        dept_name VARCHAR(50) NOT NULL UNIQUE

    )

    """)

    connection.commit()

    print("Department table created successfully.")

    cursor.close()

    connection.close()


def main():

    create_department_table()


if __name__ == "__main__":

    main()
```

---

## Output

```
Department table created successfully.
```

---

# Program-2

# Create Student Table

## What are we doing?

Creating the Student table.

Every student belongs to one department.

---

## Why?

The **dept_id** is stored as a Foreign Key.

It connects the Student table with the Department table.

---

## Complete Code

```python
from database import get_connection


def create_student_table():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    CREATE TABLE IF NOT EXISTS Student(

        student_id INT AUTO_INCREMENT PRIMARY KEY,

        student_name VARCHAR(100) NOT NULL,

        dept_id INT,

        FOREIGN KEY(dept_id)

        REFERENCES Department(dept_id)

    )

    """)

    connection.commit()

    print("Student table created successfully.")

    cursor.close()

    connection.close()


def main():

    create_student_table()


if __name__ == "__main__":

    main()
```

---

## Output

```
Student table created successfully.
```

---

# Program-3

# Create Course Table

## What are we doing?

Creating the Course table.

This table stores available courses.

---

## Why?

Instead of writing course names inside the Student table,

they are stored separately.

---

## Complete Code

```python
from database import get_connection


def create_course_table():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    CREATE TABLE IF NOT EXISTS Course(

        course_id INT AUTO_INCREMENT PRIMARY KEY,

        course_name VARCHAR(100) NOT NULL

    )

    """)

    connection.commit()

    print("Course table created successfully.")

    cursor.close()

    connection.close()


def main():

    create_course_table()


if __name__ == "__main__":

    main()
```

---

## Output

```
Course table created successfully.
```

---

# Program-4

# Create Enrollment Table

## What are we doing?

Creating the Enrollment table.

This table connects Students and Courses.

---

## Why?

A student can study many courses.

A course can have many students.

This is called a **Many-to-Many Relationship**.

---

## Complete Code

```python
from database import get_connection


def create_enrollment_table():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    CREATE TABLE IF NOT EXISTS Enrollment(

        student_id INT,

        course_id INT,

        PRIMARY KEY(student_id, course_id),

        FOREIGN KEY(student_id)

        REFERENCES Student(student_id),

        FOREIGN KEY(course_id)

        REFERENCES Course(course_id)

    )

    """)

    connection.commit()

    print("Enrollment table created successfully.")

    cursor.close()

    connection.close()


def main():

    create_enrollment_table()


if __name__ == "__main__":

    main()
```

---

## Output

```
Enrollment table created successfully.
```

---

# Program-5

# Insert Sample Departments

## What are we doing?

Adding department records.

---

## Complete Code

```python
from database import get_connection


def insert_departments():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """

    INSERT INTO Department(dept_name)

    VALUES(%s)

    """

    departments = [

        ("CSE",),

        ("ECE",),

        ("IT",)

    ]

    cursor.executemany(sql, departments)

    connection.commit()

    print("Departments inserted successfully.")

    cursor.close()

    connection.close()


def main():

    insert_departments()


if __name__ == "__main__":

    main()
```

---

## Output

```
Departments inserted successfully.
```

---

# Program-6

# Insert Sample Students

## What are we doing?

Adding students with Department IDs.

---

## Complete Code

```python
from database import get_connection


def insert_students():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """

    INSERT INTO Student(student_name, dept_id)

    VALUES(%s, %s)

    """

    students = [

        ("Alex",1),

        ("John",2),

        ("Mary",3),

        ("David",1),

        ("Priya",1)

    ]

    cursor.executemany(sql, students)

    connection.commit()

    print("Students inserted successfully.")

    cursor.close()

    connection.close()


def main():

    insert_students()


if __name__ == "__main__":

    main()
```

---

## Output

```
Students inserted successfully.
```

---

# Program-7

# Insert Sample Courses

## What are we doing?

Adding courses.

---

## Complete Code

```python
from database import get_connection


def insert_courses():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """

    INSERT INTO Course(course_name)

    VALUES(%s)

    """

    courses = [

        ("Python",),

        ("Java",),

        ("SQL",),

        ("Machine Learning",)

    ]

    cursor.executemany(sql, courses)

    connection.commit()

    print("Courses inserted successfully.")

    cursor.close()

    connection.close()


def main():

    insert_courses()


if __name__ == "__main__":

    main()
```

---

## Output

```
Courses inserted successfully.
```

---

# Program-8

# Insert Enrollment Records

## What are we doing?

Connecting students with courses.

---

## Complete Code

```python
from database import get_connection


def insert_enrollments():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """

    INSERT INTO Enrollment(student_id, course_id)

    VALUES(%s, %s)

    """

    enrollments = [

        (1,1),

        (1,3),

        (2,2),

        (3,1),

        (4,4),

        (5,1),

        (5,2)

    ]

    cursor.executemany(sql, enrollments)

    connection.commit()

    print("Enrollment records inserted successfully.")

    cursor.close()

    connection.close()


def main():

    insert_enrollments()


if __name__ == "__main__":

    main()
```

---

## Output

```
Enrollment records inserted successfully.
```

---

# Summary

In this part, we completed:

- Create Department Table
- Create Student Table
- Create Course Table
- Create Enrollment Table
- Insert Department Records
- Insert Student Records
- Insert Course Records
- Insert Enrollment Records

The database is now ready for learning different types of **JOIN** operations in Part-2.
