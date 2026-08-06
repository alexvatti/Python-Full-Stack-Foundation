# Program-1

# COUNT()

## What does it do?

The **COUNT()** function returns the total number of records in a table.

---

## Why do we use COUNT()?

Suppose a company wants to know

- Total Employees
- Total Students
- Total Products

Instead of counting manually, SQL does it automatically.

---

## We Want

Count the total number of employees.

---

## Employee Table

| ID | Name | Department | Salary |
|----|------|------------|-------:|
|1|Alex|IT|65000|
|2|John|HR|45000|
|3|David|IT|70000|
|4|Mary|Sales|55000|
|5|Neha|HR|50000|

---

## Complete Code

```python
from database import get_connection


def count_employees():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT COUNT(*)
    FROM Employee
    """)

    total = cursor.fetchone()

    print("Total Employees :", total[0])

    cursor.close()
    connection.close()


def main():

    count_employees()


if __name__ == "__main__":
    main()
```

---

## Output

```
Total Employees : 5
```

---

# Program-2

# SUM()

## What does it do?

Calculates the total of all salary values.

---

## Why do we use SUM()?

Useful for finding

- Total Salary
- Total Sales
- Total Revenue
- Total Expenses

---

## We Want

Calculate the total salary of all employees.

---

## Complete Code

```python
from database import get_connection


def total_salary():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT SUM(salary)
    FROM Employee
    """)

    total = cursor.fetchone()

    print("Total Salary :", total[0])

    cursor.close()
    connection.close()


def main():

    total_salary()


if __name__ == "__main__":
    main()
```

---

## Output

```
Total Salary : 285000
```

---

# Program-3

# AVG()

## What does it do?

Calculates the average salary.

---

## Why do we use AVG()?

Used to find

- Average Salary
- Average Marks
- Average Price

---

## We Want

Display the average salary.

---

## Complete Code

```python
from database import get_connection


def average_salary():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT AVG(salary)
    FROM Employee
    """)

    average = cursor.fetchone()

    print("Average Salary :", average[0])

    cursor.close()
    connection.close()


def main():

    average_salary()


if __name__ == "__main__":
    main()
```

---

## Output

```
Average Salary : 57000.00
```

---

# Program-4

# MIN() and MAX()

## What does it do?

Finds the minimum and maximum salary.

---

## Why do we use MIN() and MAX()?

Useful for

- Lowest Salary
- Highest Salary
- Lowest Marks
- Highest Marks

---

## We Want

Display the lowest and highest salary.

---

## Complete Code

```python
from database import get_connection


def salary_statistics():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT
    MIN(salary),
    MAX(salary)
    FROM Employee
    """)

    result = cursor.fetchone()

    print("Lowest Salary  :", result[0])
    print("Highest Salary :", result[1])

    cursor.close()
    connection.close()


def main():

    salary_statistics()


if __name__ == "__main__":
    main()
```

---

## Output

```
Lowest Salary  : 45000
Highest Salary : 70000
```

---

# Program-5

# DISTINCT

## What does it do?

Removes duplicate department names.

---

## Why do we use DISTINCT?

Useful for displaying unique values.

---

## We Want

Display all unique departments.

---

## Complete Code

```python
from database import get_connection


def distinct_departments():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT DISTINCT department
    FROM Employee
    """)

    rows = cursor.fetchall()

    print("Departments")
    print("-----------")

    for row in rows:
        print(row[0])

    cursor.close()
    connection.close()


def main():

    distinct_departments()


if __name__ == "__main__":
    main()
```

---

## Output

```
Departments
-----------
IT
HR
Sales
```

---

# Program-6

# GROUP BY

## What does it do?

Groups employees department-wise.

---

## Why do we use GROUP BY?

Useful for generating department-wise reports.

---

## We Want

Display employee count in each department.

---

## Complete Code

```python
from database import get_connection


def group_by_department():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT
    department,
    COUNT(*)
    FROM Employee
    GROUP BY department
    """)

    rows = cursor.fetchall()

    print("Department\tEmployees")
    print("-------------------------")

    for row in rows:
        print(row[0],"\t\t",row[1])

    cursor.close()
    connection.close()


def main():

    group_by_department()


if __name__ == "__main__":
    main()
```

---

## Output

```
Department      Employees
-------------------------
HR              2
IT              2
Sales           1
```

---

# Program-7

# HAVING

## What does it do?

Filters grouped records.

---

## Why do we use HAVING?

Used after GROUP BY.

---

## We Want

Display departments having more than one employee.

---

## Complete Code

```python
from database import get_connection


def having_clause():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT
    department,
    COUNT(*)
    FROM Employee
    GROUP BY department
    HAVING COUNT(*) > 1
    """)

    rows = cursor.fetchall()

    print("Departments")
    print("-----------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    having_clause()


if __name__ == "__main__":
    main()
```

---

## Output

```
('HR', 2)

('IT', 2)
```

---

# Program-8

# String Functions

## What does it do?

Performs operations on text.

---

## We Want

Display employee names in uppercase.

---

## Complete Code

```python
from database import get_connection


def string_functions():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT
    name,
    UPPER(name),
    LOWER(name),
    LENGTH(name)
    FROM Employee
    """)

    rows = cursor.fetchall()

    print("Name\tUpper\tLower\tLength")
    print("-----------------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    string_functions()


if __name__ == "__main__":
    main()
```

---

## Output

```
('Alex', 'ALEX', 'alex', 4)
('John', 'JOHN', 'john', 4)
('David', 'DAVID', 'david', 5)
...
```

---

# Program-9

# Numeric Functions

## What does it do?

Performs mathematical calculations.

---

## We Want

Display various numeric function results.

---

## Complete Code

```python
from database import get_connection


def numeric_functions():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT
    ROUND(AVG(salary),2),
    CEIL(25.2),
    FLOOR(25.9),
    ABS(-500),
    MOD(17,5),
    POWER(2,5),
    SQRT(81)
    FROM Employee
    """)

    row = cursor.fetchone()

    print(row)

    cursor.close()
    connection.close()


def main():

    numeric_functions()


if __name__ == "__main__":
    main()
```

---

## Output

```
(57000.00, 26, 25, 500, 2, 32, 9)
```

---

# Program-10

# Date Functions

## What does it do?

Displays current date and time information.

---

## We Want

Display today's date and related values.

---

## Complete Code

```python
from database import get_connection


def date_functions():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT
    CURDATE(),
    CURTIME(),
    NOW(),
    YEAR(CURDATE()),
    MONTH(CURDATE()),
    DAY(CURDATE())
    """)

    row = cursor.fetchone()

    print(row)

    cursor.close()
    connection.close()


def main():

    date_functions()


if __name__ == "__main__":
    main()
```

---

## Sample Output

```
(datetime.date(2026, 8, 6),
 datetime.time(11, 25, 30),
 datetime.datetime(2026, 8, 6, 11, 25, 30),
 2026,
 8,
 6)
```

---

# Program-11

# Complete Employee Report

## What does it do?

Generates a complete department-wise salary report.

---

## We Want

Display

- Department
- Employee Count
- Total Salary
- Average Salary
- Lowest Salary
- Highest Salary

---

## Complete Code

```python
from database import get_connection


def employee_report():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT
    department,
    COUNT(*) AS Employees,
    SUM(salary) AS TotalSalary,
    AVG(salary) AS AverageSalary,
    MIN(salary) AS LowestSalary,
    MAX(salary) AS HighestSalary
    FROM Employee
    GROUP BY department
    ORDER BY AverageSalary DESC
    """)

    rows = cursor.fetchall()

    print("Department\tEmployees\tTotal\tAverage\tLowest\tHighest")
    print("---------------------------------------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    employee_report()


if __name__ == "__main__":
    main()
```

---

## Output

```
('IT', 2, 135000, 67500.0000, 65000, 70000)

('Sales', 1, 55000, 55000.0000, 55000, 55000)

('HR', 2, 95000, 47500.0000, 45000, 50000)
```
