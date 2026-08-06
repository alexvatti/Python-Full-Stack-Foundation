# Python Full Stack Foundation

# Week-07 – Day-35

# Part-2

# MySQL Database

# JOIN Operations

## Using Modular Programming

---

# Objective

In Part-1, we created the following tables.

```
Department

↓

Student

↓

Enrollment

↓

Course
```

Now, we will retrieve data from multiple tables using different types of JOINs.

All programs use the common database connection.

```python
from database import get_connection
```

---

# Current Database

## Department

| Dept_ID | Department |
|---------:|------------|
|1|CSE|
|2|ECE|
|3|IT|

---

## Student

| Student_ID | Student | Dept_ID |
|-----------:|---------|---------:|
|1|Alex|1|
|2|John|2|
|3|Mary|3|
|4|David|1|
|5|Priya|1|

---

## Course

| Course_ID | Course |
|----------:|--------|
|1|Python|
|2|Java|
|3|SQL|
|4|Machine Learning|

---

## Enrollment

| Student_ID | Course_ID |
|-----------:|----------:|
|1|1|
|1|3|
|2|2|
|3|1|
|4|4|
|5|1|
|5|2|

---

# Program-1

# INNER JOIN

## What are we doing?

Display every student along with their department.

---

## Why?

The Student table contains only the Department ID.

INNER JOIN retrieves the department name from the Department table.

---

## Complete Code

```python
from database import get_connection


def inner_join():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    SELECT

        Student.student_name,

        Department.dept_name

    FROM Student

    INNER JOIN Department

    ON Student.dept_id = Department.dept_id

    """)

    rows = cursor.fetchall()

    print("Student\tDepartment")
    print("--------------------------")

    for row in rows:
        print(row[0], "\t", row[1])

    cursor.close()

    connection.close()


def main():

    inner_join()


if __name__ == "__main__":

    main()
```

---

## Output

```
Student     Department
--------------------------
Alex        CSE
John        ECE
Mary        IT
David       CSE
Priya       CSE
```

---

# Program-2

# LEFT JOIN

## What are we doing?

Display all students even if a department is missing.

---

## Why?

LEFT JOIN always displays all records from the left table.

---

## Complete Code

```python
from database import get_connection


def left_join():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    SELECT

        Student.student_name,

        Department.dept_name

    FROM Student

    LEFT JOIN Department

    ON Student.dept_id = Department.dept_id

    """)

    rows = cursor.fetchall()

    print("Student\tDepartment")
    print("--------------------------")

    for row in rows:
        print(row)

    cursor.close()

    connection.close()


def main():

    left_join()


if __name__ == "__main__":

    main()
```

---

## Output

```
('Alex', 'CSE')
('John', 'ECE')
('Mary', 'IT')
('David', 'CSE')
('Priya', 'CSE')
```

---

# Program-3

# RIGHT JOIN

## What are we doing?

Display all departments even if there are no students.

---

## Why?

RIGHT JOIN always displays all records from the right table.

---

## Complete Code

```python
from database import get_connection


def right_join():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    SELECT

        Student.student_name,

        Department.dept_name

    FROM Student

    RIGHT JOIN Department

    ON Student.dept_id = Department.dept_id

    """)

    rows = cursor.fetchall()

    print("Student\tDepartment")
    print("--------------------------")

    for row in rows:
        print(row)

    cursor.close()

    connection.close()


def main():

    right_join()


if __name__ == "__main__":

    main()
```

---

## Output

```
('Alex', 'CSE')
('David', 'CSE')
('Priya', 'CSE')
('John', 'ECE')
('Mary', 'IT')
```

---

# Program-4

# CROSS JOIN

## What are we doing?

Display every possible combination of Students and Courses.

---

## Why?

Useful for generating all combinations.

Formula

```
Rows in Student

×

Rows in Course
```

---

## Complete Code

```python
from database import get_connection


def cross_join():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    SELECT

        Student.student_name,

        Course.course_name

    FROM Student

    CROSS JOIN Course

    """)

    rows = cursor.fetchall()

    print("Student\tCourse")
    print("--------------------------")

    for row in rows:
        print(row)

    cursor.close()

    connection.close()


def main():

    cross_join()


if __name__ == "__main__":

    main()
```

---

## Sample Output

```
Alex     Python
Alex     Java
Alex     SQL
Alex     Machine Learning
John     Python
John     Java
...
```

Total Records

```
5 × 4 = 20
```

---

# Program-5

# Student with Courses

## What are we doing?

Display every student along with the courses they enrolled in.

---

## Why?

This query combines three tables.

- Student
- Enrollment
- Course

---

## Complete Code

```python
from database import get_connection


def student_courses():

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
    print("--------------------------")

    for row in rows:
        print(row)

    cursor.close()

    connection.close()


def main():

    student_courses()


if __name__ == "__main__":

    main()
```

---

## Output

```
Alex      Python
Alex      SQL
David     Machine Learning
John      Java
Mary      Python
Priya     Python
Priya     Java
```

---

# Program-6

# Student, Department and Course

## What are we doing?

Generate a complete student report.

---

## Why?

Combine all four tables into one report.

---

## Complete Code

```python
from database import get_connection


def complete_report():

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

    ORDER BY Student.student_name

    """)

    rows = cursor.fetchall()

    print("Student\tDepartment\tCourse")
    print("---------------------------------------------")

    for row in rows:
        print(row)

    cursor.close()

    connection.close()


def main():

    complete_report()


if __name__ == "__main__":

    main()
```

---

## Output

```
Alex      CSE      Python
Alex      CSE      SQL
David     CSE      Machine Learning
John      ECE      Java
Mary      IT       Python
Priya     CSE      Python
Priya     CSE      Java
```

---

# Program-7

# Department-wise Student Count

## What are we doing?

Count the number of students in each department.

---

## Why?

This is a practical report using JOIN with GROUP BY.

---

## Complete Code

```python
from database import get_connection


def department_report():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""

    SELECT

        Department.dept_name,

        COUNT(Student.student_id)

    FROM Department

    LEFT JOIN Student

    ON Department.dept_id = Student.dept_id

    GROUP BY Department.dept_name

    ORDER BY Department.dept_name

    """)

    rows = cursor.fetchall()

    print("Department\tStudents")
    print("---------------------------")

    for row in rows:
        print(row)

    cursor.close()

    connection.close()


def main():

    department_report()


if __name__ == "__main__":

    main()
```

---

## Output

```
('CSE', 3)
('ECE', 1)
('IT', 1)
```

---

# Summary

In this part, we learned:

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- CROSS JOIN
- Multi-table INNER JOIN
- Student-Course Report
- Student-Department-Course Report
- Department-wise Student Report

All programs use the reusable `database.py` connection module developed in the previous sessions.
