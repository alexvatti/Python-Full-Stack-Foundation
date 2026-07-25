# Python Full Stack Foundation

# Week-07 – Day-34

# MySQL Database

# Aggregate Functions, GROUP BY, HAVING & Built-in Functions

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
- Use GROUP BY
- Use HAVING
- Use MySQL String Functions
- Use MySQL Numeric Functions
- Use MySQL Date Functions
- Generate Reports using SQL

---

# Agenda

1. Aggregate Functions
2. COUNT()
3. SUM()
4. AVG()
5. MIN()
6. MAX()
7. DISTINCT
8. GROUP BY
9. HAVING
10. String Functions
11. Numeric Functions
12. Date Functions
13. Report Generation

---

# Recap

Previous Session

✓ INSERT

✓ SELECT

✓ UPDATE

✓ DELETE

✓ ORDER BY

✓ LIMIT

✓ CRUD Operations

Today we learn how SQL is used to generate reports and perform data analysis.

---

# Sample Employee Table

| Emp_ID | Name | Department | Salary |
|---------|------|------------|--------:|
|1|Alex|IT|65000|
|2|John|HR|45000|
|3|David|IT|70000|
|4|Mary|Sales|55000|
|5|Neha|HR|50000|

---

# What are Aggregate Functions?

## Definition

Aggregate Functions perform calculations on multiple rows and return a **single value**.

Instead of displaying every record,

they summarize the data.

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

# COUNT()

## Definition

Returns the number of rows.

---

## Syntax

```sql
SELECT COUNT(*)

FROM Employee;
```

Output

```
5
```

---

# COUNT(Column)

```sql
SELECT COUNT(salary)

FROM Employee;
```

Counts only non-NULL salary values.

---

# COUNT(DISTINCT)

```sql
SELECT COUNT(DISTINCT department)

FROM Employee;
```

Output

```
3
```

Departments

```
IT

HR

Sales
```

---

# SUM()

## Definition

Adds all numeric values.

---

Example

```sql
SELECT SUM(salary)

FROM Employee;
```

Output

```
285000
```

---

# AVG()

## Definition

Returns the average value.

---

Example

```sql
SELECT AVG(salary)

FROM Employee;
```

Output

```
57000
```

---

# MIN()

Returns the smallest value.

```sql
SELECT MIN(salary)

FROM Employee;
```

Output

```
45000
```

---

# MAX()

Returns the highest value.

```sql
SELECT MAX(salary)

FROM Employee;
```

Output

```
70000
```

---

# Display Complete Statistics

```sql
SELECT

COUNT(*) AS Employees,

SUM(salary) AS TotalSalary,

AVG(salary) AS AverageSalary,

MIN(salary) AS LowestSalary,

MAX(salary) AS HighestSalary

FROM Employee;
```

Output

```
Employees : 5

Total Salary : 285000

Average Salary : 57000

Lowest Salary : 45000

Highest Salary : 70000
```

---

# DISTINCT

## Definition

Removes duplicate values.

---

Without DISTINCT

```sql
SELECT department

FROM Employee;
```

Output

```
IT

HR

IT

Sales

HR
```

---

With DISTINCT

```sql
SELECT DISTINCT department

FROM Employee;
```

Output

```
IT

HR

Sales
```

---

# GROUP BY

## Definition

Groups rows having the same values.

---

Example

```sql
SELECT

department,

COUNT(*)

FROM Employee

GROUP BY department;
```

Output

| Department | Employees |
|------------|----------:|
|HR|2|
|IT|2|
|Sales|1|

---

# Average Salary by Department

```sql
SELECT

department,

AVG(salary)

FROM Employee

GROUP BY department;
```

---

# Total Salary by Department

```sql
SELECT

department,

SUM(salary)

FROM Employee

GROUP BY department;
```

Output

| Department | Total Salary |
|------------|-------------:|
|HR|95000|
|IT|135000|
|Sales|55000|

---

# Maximum Salary by Department

```sql
SELECT

department,

MAX(salary)

FROM Employee

GROUP BY department;
```

---

# HAVING

## Definition

HAVING filters grouped records.

WHERE filters individual rows.

---

# WHERE vs HAVING

| WHERE | HAVING |
|---------|---------|
| Before GROUP BY | After GROUP BY |
| Filters rows | Filters groups |

---

# Example

Departments having more than one employee.

```sql
SELECT

department,

COUNT(*)

FROM Employee

GROUP BY department

HAVING COUNT(*)>1;
```

Output

```
HR

IT
```

---

# Example

Departments with average salary above 60000.

```sql
SELECT

department,

AVG(salary)

FROM Employee

GROUP BY department

HAVING AVG(salary)>60000;
```

Output

```
IT
```

---

# ORDER BY with GROUP BY

```sql
SELECT

department,

AVG(salary)

AS AverageSalary

FROM Employee

GROUP BY department

ORDER BY AverageSalary DESC;
```

---

# Aliases (AS)

Aliases improve readability.

```sql
SELECT

AVG(salary) AS AverageSalary

FROM Employee;
```

Instead of

```
AVG(salary)
```

Output displays

```
AverageSalary
```

---

# String Functions

String Functions manipulate text.

---

# UPPER()

Converts text to uppercase.

```sql
SELECT

UPPER(name)

FROM Employee;
```

Output

```
ALEX

JOHN

DAVID
```

---

# LOWER()

```sql
SELECT

LOWER(name)

FROM Employee;
```

---

# LENGTH()

Returns string length.

```sql
SELECT

name,

LENGTH(name)

FROM Employee;
```

Output

```
Alex    4

David   5
```

---

# CONCAT()

Joins strings.

```sql
SELECT

CONCAT(name,' - ',department)

FROM Employee;
```

Output

```
Alex - IT

John - HR
```

---

# LEFT()

Returns left characters.

```sql
SELECT

LEFT(name,3)

FROM Employee;
```

Output

```
Ale

Joh

Dav
```

---

# RIGHT()

```sql
SELECT

RIGHT(name,2)

FROM Employee;
```

---

# SUBSTRING()

```sql
SELECT

SUBSTRING(name,2,3)

FROM Employee;
```

---

# TRIM()

Removes spaces.

```sql
SELECT

TRIM('   Alex   ');
```

Output

```
Alex
```

---

# REPLACE()

```sql
SELECT

REPLACE('Python SQL','SQL','MySQL');
```

Output

```
Python MySQL
```

---

# Numeric Functions

---

# ROUND()

```sql
SELECT

ROUND(AVG(salary),2)

FROM Employee;
```

---

# CEIL()

Rounds upward.

```sql
SELECT CEIL(25.2);
```

Output

```
26
```

---

# FLOOR()

Rounds downward.

```sql
SELECT FLOOR(25.9);
```

Output

```
25
```

---

# ABS()

Returns absolute value.

```sql
SELECT ABS(-500);
```

Output

```
500
```

---

# MOD()

Returns remainder.

```sql
SELECT MOD(17,5);
```

Output

```
2
```

---

# POWER()

```sql
SELECT POWER(2,5);
```

Output

```
32
```

---

# SQRT()

```sql
SELECT SQRT(81);
```

Output

```
9
```

---

# Date Functions

---

# CURDATE()

Returns today's date.

```sql
SELECT CURDATE();
```

Example

```
2026-08-25
```

---

# CURTIME()

```sql
SELECT CURTIME();
```

---

# NOW()

Returns current date and time.

```sql
SELECT NOW();
```

---

# YEAR()

```sql
SELECT

YEAR(CURDATE());
```

---

# MONTH()

```sql
SELECT MONTH(CURDATE());
```

---

# DAY()

```sql
SELECT DAY(CURDATE());
```

---

# DATEDIFF()

```sql
SELECT

DATEDIFF('2026-12-31','2026-08-25');
```

Returns difference in days.

---

# DATE_ADD()

```sql
SELECT

DATE_ADD(CURDATE(),

INTERVAL 30 DAY);
```

---

# DATE_SUB()

```sql
SELECT

DATE_SUB(CURDATE(),

INTERVAL 15 DAY);
```

---

# Complete Employee Report

```sql
SELECT

department,

COUNT(*) AS Employees,

SUM(salary) AS TotalSalary,

AVG(salary) AS AverageSalary,

MIN(salary) AS Lowest,

MAX(salary) AS Highest

FROM Employee

GROUP BY department

ORDER BY AverageSalary DESC;
```

---

# Product Report

```sql
SELECT

category,

COUNT(*) AS Products,

AVG(price),

SUM(quantity)

FROM Product

GROUP BY category;
```

---

# Student Report

```sql
SELECT

department,

COUNT(*),

AVG(marks),

MAX(marks),

MIN(marks)

FROM Student

GROUP BY department;
```

---

# Sales Report

```sql
SELECT

MONTH(order_date),

SUM(amount)

FROM Sales

GROUP BY MONTH(order_date);
```

---

# Function Categories

```
Functions

│

├── Aggregate

├── String

├── Numeric

└── Date
```

---

# Best Practices

✓ Use aliases (AS).

✓ Use GROUP BY for reports.

✓ Use HAVING after GROUP BY.

✓ Use ROUND() for averages.

✓ Write SQL keywords in uppercase.

---

# Common Mistakes

❌ Forgetting GROUP BY.

Incorrect

```sql
SELECT department,

AVG(salary)

FROM Employee;
```

Correct

```sql
SELECT department,

AVG(salary)

FROM Employee

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

❌ Using COUNT(column) when NULL values exist unexpectedly.

---

# Practice Exercises

## Exercise 1

Count total employees.

---

## Exercise 2

Find total salary.

---

## Exercise 3

Find average salary.

---

## Exercise 4

Find highest salary.

---

## Exercise 5

Display all unique departments.

---

## Exercise 6

Generate department-wise employee count.

---

## Exercise 7

Generate department-wise average salary.

---

## Exercise 8

Display departments having more than one employee.

---

## Exercise 9

Display employee names in uppercase.

---

## Exercise 10

Generate a complete salary report using GROUP BY.

---

# Interview Questions

### 1. What is the difference between COUNT(*) and COUNT(column)?

### 2. Why do we use GROUP BY?

### 3. What is HAVING?

### 4. Difference between WHERE and HAVING?

### 5. Name five aggregate functions.

### 6. What does CONCAT() do?

### 7. Difference between ROUND() and FLOOR()?

### 8. Difference between CURDATE() and NOW()?

### 9. Why are aliases used?

### 10. Give three examples of String Functions.

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

✓ GROUP BY

✓ HAVING

✓ Aliases

✓ String Functions

✓ Numeric Functions

✓ Date Functions

✓ SQL Reports

---

# Coming Next (Day-35)

- Table Relationships
- PRIMARY KEY & FOREIGN KEY
- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- SELF JOIN
- CROSS JOIN
- Database Normalization
- Complete College Database Project
- Mini Project (MySQL + Python)
