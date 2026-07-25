# Python Full Stack Foundation

# Week-06 – Day-29

# SQLite Database Programming

# Aggregate Functions, Filtering & Data Analysis

**Level:** Beginner → Intermediate

**Duration:** 2–3 Hours

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Aggregate Functions
- Use COUNT()
- Use SUM()
- Use AVG()
- Use MIN()
- Use MAX()
- Use DISTINCT
- Use LIKE
- Use Wildcards
- Use BETWEEN
- Use IN
- Use GROUP BY
- Use HAVING
- Generate Summary Reports
- Perform Data Analysis using SQL

---

# Agenda

1. Aggregate Functions
2. COUNT()
3. SUM()
4. AVG()
5. MIN()
6. MAX()
7. DISTINCT
8. LIKE
9. BETWEEN
10. IN
11. GROUP BY
12. HAVING
13. Reporting Queries

---

# Recap

Previous Session

✓ INSERT

✓ SELECT

✓ UPDATE

✓ DELETE

✓ WHERE

✓ ORDER BY

✓ LIMIT

✓ Parameterized Queries

Today we learn how to analyse data using SQL.

---

# Sample Student Table

| ID | Name | Department | Marks |
|----|------|------------|------:|
|1|Alex|CSE|91|
|2|John|ECE|85|
|3|Ravi|CSE|75|
|4|Priya|IT|94|
|5|Neha|ECE|82|

---

# What are Aggregate Functions?

## Definition

Aggregate Functions perform calculations on multiple rows and return a single result.

Instead of returning every record,

they return one summary value.

---

# Aggregate Functions

```
Aggregate Functions

│

├── COUNT()

├── SUM()

├── AVG()

├── MIN()

└── MAX()
```

---

# Why Use Aggregate Functions?

Without Aggregate Functions

```
Read Every Record

↓

Calculate Manually
```

With Aggregate Functions

```
Single SQL Statement

↓

Instant Result
```

---

# COUNT()

## Definition

COUNT() returns the number of records.

---

# Syntax

```sql
SELECT COUNT(*)

FROM Student;
```

---

# Python Example

```python
cursor.execute("""

SELECT COUNT(*)

FROM Student

""")

count = cursor.fetchone()

print(count)
```

Output

```
(5,)
```

---

# Better Output

```python
total = cursor.fetchone()[0]

print("Total Students :", total)
```

Output

```
Total Students : 5
```

---

# COUNT(Column)

```sql
SELECT COUNT(name)

FROM Student;
```

Counts only non-NULL values.

---

# COUNT(DISTINCT)

```sql
SELECT COUNT(DISTINCT department)

FROM Student;
```

Output

```
3
```

Departments

```
CSE

ECE

IT
```

---

# SUM()

## Definition

SUM() adds all numeric values.

---

# Syntax

```sql
SELECT SUM(marks)

FROM Student;
```

---

# Python Example

```python
cursor.execute("""

SELECT SUM(marks)

FROM Student

""")

print(cursor.fetchone()[0])
```

Output

```
427
```

---

# AVG()

## Definition

AVG() returns the average value.

---

# Example

```sql
SELECT AVG(marks)

FROM Student;
```

Output

```
85.4
```

---

# Python Example

```python
cursor.execute("""

SELECT AVG(marks)

FROM Student

""")

average = cursor.fetchone()[0]

print(round(average,2))
```

Output

```
85.40
```

---

# MIN()

## Definition

Returns the smallest value.

---

Example

```sql
SELECT MIN(marks)

FROM Student;
```

Output

```
75
```

---

# MAX()

## Definition

Returns the highest value.

---

Example

```sql
SELECT MAX(marks)

FROM Student;
```

Output

```
94
```

---

# Display Complete Statistics

```python
cursor.execute("""

SELECT

COUNT(*),

AVG(marks),

MIN(marks),

MAX(marks)

FROM Student

""")

print(cursor.fetchone())
```

Output

```
(5,85.4,75,94)
```

---

# DISTINCT

## Definition

DISTINCT removes duplicate values.

---

Example

```sql
SELECT department

FROM Student;
```

Output

```
CSE

ECE

CSE

IT

ECE
```

---

Using DISTINCT

```sql
SELECT DISTINCT department

FROM Student;
```

Output

```
CSE

ECE

IT
```

---

# LIKE

## Definition

LIKE searches for patterns.

---

# Wildcards

| Symbol | Meaning |
|----------|----------|
| % | Any number of characters |
| _ | Single character |

---

# Example

Names beginning with A

```sql
SELECT *

FROM Student

WHERE name LIKE 'A%';
```

Output

```
Alex
```

---

# Ending Pattern

Names ending with a

```sql
SELECT *

FROM Student

WHERE name LIKE '%a';
```

---

# Contains

Names containing "ri"

```sql
SELECT *

FROM Student

WHERE name LIKE '%ri%';
```

Output

```
Priya
```

---

# Single Character

```sql
SELECT *

FROM Student

WHERE name LIKE '_lex';
```

Matches

```
Alex
```

---

# BETWEEN

## Definition

BETWEEN selects values within a range.

---

Example

```sql
SELECT *

FROM Student

WHERE marks

BETWEEN 80 AND 90;
```

Output

```
John

Neha
```

---

# Date Example

```sql
SELECT *

FROM Orders

WHERE order_date

BETWEEN

'2025-01-01'

AND

'2025-12-31';
```

---

# IN Operator

## Definition

IN checks multiple values.

---

Without IN

```sql
WHERE department='CSE'

OR department='IT'
```

---

Using IN

```sql
SELECT *

FROM Student

WHERE department

IN ('CSE','IT');
```

Cleaner and easier to read.

---

# NOT IN

```sql
SELECT *

FROM Student

WHERE department

NOT IN ('ECE');
```

---

# GROUP BY

## Definition

GROUP BY groups similar records together.

---

Example

```sql
SELECT department,

COUNT(*)

FROM Student

GROUP BY department;
```

Output

| Department | Students |
|-------------|----------|
| CSE | 2 |
| ECE | 2 |
| IT | 1 |

---

# Another Example

Average Marks by Department

```sql
SELECT

department,

AVG(marks)

FROM Student

GROUP BY department;
```

Output

| Department | Average |
|-------------|---------|
| CSE | 83 |
| ECE | 83.5 |
| IT | 94 |

---

# SUM with GROUP BY

```sql
SELECT

department,

SUM(marks)

FROM Student

GROUP BY department;
```

---

# HAVING

## Definition

HAVING filters grouped data.

WHERE filters individual rows.

HAVING filters groups.

---

# WHERE vs HAVING

| WHERE | HAVING |
|---------|---------|
| Before GROUP BY | After GROUP BY |
| Individual Rows | Groups |

---

# Example

```sql
SELECT

department,

COUNT(*)

FROM Student

GROUP BY department

HAVING COUNT(*)>1;
```

Output

```
CSE

ECE
```

---

# Another Example

Departments having average marks above 85.

```sql
SELECT

department,

AVG(marks)

FROM Student

GROUP BY department

HAVING AVG(marks)>85;
```

Output

```
IT
```

---

# Complete Report

```sql
SELECT

department,

COUNT(*) AS Students,

AVG(marks) AS Average,

MIN(marks) AS Lowest,

MAX(marks) AS Highest

FROM Student

GROUP BY department;
```

---

# Employee Example

Table

| Name | Department | Salary |
|------|------------|-------:|
|Alex|HR|35000|
|John|IT|60000|
|David|IT|55000|
|Mary|HR|42000|

---

Total Salary

```sql
SELECT

SUM(salary)

FROM Employee;
```

---

Average Salary

```sql
SELECT

AVG(salary)

FROM Employee;
```

---

Salary by Department

```sql
SELECT

department,

SUM(salary)

FROM Employee

GROUP BY department;
```

---

# Product Example

| Product | Price | Quantity |
|----------|------:|---------:|
|Laptop|65000|5|
|Mouse|500|25|
|Keyboard|1500|10|

Highest Price

```sql
SELECT MAX(price)

FROM Product;
```

---

Lowest Price

```sql
SELECT MIN(price)

FROM Product;
```

---

# Library Example

Books issued by category.

```sql
SELECT

category,

COUNT(*)

FROM Book

GROUP BY category;
```

---

# Hospital Example

Patients by Disease

```sql
SELECT

disease,

COUNT(*)

FROM Patient

GROUP BY disease;
```

---

# Banking Example

Total Balance

```sql
SELECT

SUM(balance)

FROM Account;
```

---

# Sales Example

Average Monthly Sales

```sql
SELECT

AVG(amount)

FROM Sales;
```

---

# Mini Dashboard Query

```sql
SELECT

COUNT(*) AS Students,

AVG(marks) AS Average,

MIN(marks) AS Lowest,

MAX(marks) AS Highest

FROM Student;
```

Output

```
Students : 5

Average : 85.4

Lowest : 75

Highest : 94
```

---

# Query Execution Flow

```
Table

↓

Filter (WHERE)

↓

Group (GROUP BY)

↓

Aggregate

↓

HAVING

↓

Result
```

---

# Best Practices

✓ Use COUNT(*) for total records.

✓ Use GROUP BY for reports.

✓ Use HAVING only with grouped data.

✓ Use DISTINCT to remove duplicates.

✓ Use aliases for readable reports.

✓ Write SQL keywords in uppercase.

---

# Common Mistakes

❌ Using HAVING without GROUP BY when unnecessary.

❌ Forgetting GROUP BY while selecting non-aggregated columns.

Incorrect

```sql
SELECT department,

AVG(marks)

FROM Student;
```

Correct

```sql
SELECT department,

AVG(marks)

FROM Student

GROUP BY department;
```

---

❌ Confusing WHERE and HAVING.

WHERE

↓

Before grouping

HAVING

↓

After grouping

---

# Practice Exercises

## Exercise 1

Count total students.

---

## Exercise 2

Find highest marks.

---

## Exercise 3

Find lowest salary.

---

## Exercise 4

Display all unique departments.

---

## Exercise 5

Find students scoring between 70 and 90.

---

## Exercise 6

Display students whose names start with "P".

---

## Exercise 7

Display students from CSE and IT departments.

---

## Exercise 8

Count students in each department.

---

## Exercise 9

Display departments having more than one student.

---

## Exercise 10

Generate a report showing

- Department
- Student Count
- Average Marks
- Highest Marks
- Lowest Marks

---

# Summary

Today we learned

✓ Aggregate Functions

✓ COUNT()

✓ SUM()

✓ AVG()

✓ MIN()

✓ MAX()

✓ DISTINCT

✓ LIKE

✓ Wildcards

✓ BETWEEN

✓ IN

✓ GROUP BY

✓ HAVING

✓ SQL Reports

✓ Data Analysis Queries

---

# Coming Next (Day-30)

- Database Relationships
- Primary Key
- Foreign Key
- Constraints
- One-to-One Relationship
- One-to-Many Relationship
- Many-to-Many Relationship
- Joins (Introduction)
- Database Design
- Complete College Database Design
