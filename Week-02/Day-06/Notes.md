# Python Full Stack Foundation

# Week 2 – Day 6

## if Statement, Conditions, Indentation

---

# Learning Objectives

By the end of this session, learners will be able to:

* Understand Decision Making
* Understand Conditions
* Use the `if` Statement
* Understand Indentation
* Build Basic Decision-Making Programs
* Create Eligibility Checkers
* Solve Real-World Problems Using Conditions

---

# Recap of Week 1

Previously we learned:

* Variables
* Data Types
* Input and Output
* Type Casting
* Arithmetic Operators
* Assignment Operators
* Relational Operators
* Logical Operators
* Expressions
* Operator Precedence

Until now our programs executed every line.

Today we will learn how programs can make decisions.

---

# 1. What is Decision Making?

Decision Making means:

```text
Perform an action only when a condition is True.
```

---

# Real-Life Examples

## Example 1

If it rains,

```text
Take Umbrella
```

---

## Example 2

If you are hungry,

```text
Eat Food
```

---

## Example 3

If age is 18 or above,

```text
Eligible for Voting
```

---

## Example 4

If marks are above 35,

```text
Student Passed
```

---

# Decision Making in Programming

Programs also make decisions.

Example:

```text
If age >= 18
Display Eligible for Voting
```

---

# 2. What is a Condition?

A Condition is an expression that returns:

```text
True
or
False
```

---

## Examples

```python
10 > 5
```

Output

```text
True
```

---

```python
20 < 10
```

Output

```text
False
```

---

```python
100 == 100
```

Output

```text
True
```

---

# More Conditions

```python
age >= 18
```

```python
salary > 50000
```

```python
marks >= 35
```

```python
attendance >= 75
```

All these conditions return:

```text
True or False
```

---

# 3. The if Statement

The `if` statement executes code only when the condition is True.

---

# Syntax

```python
if condition:
    statement
```

---

# Important

Notice the colon:

```python
:
```

after the condition.

---

# Flow

```text
Condition True
      ↓
 Execute Code

Condition False
      ↓
 Skip Code
```

---

# Example 1

```python
age = 20

if age >= 18:
    print("Eligible for Voting")
```

Output

```text
Eligible for Voting
```

---

# Example 2

```python
marks = 80

if marks >= 35:
    print("Pass")
```

Output

```text
Pass
```

---

# Example 3

```python
salary = 60000

if salary > 50000:
    print("High Income")
```

Output

```text
High Income
```

---

# Example 4

```python
temperature = 40

if temperature > 35:
    print("Hot Weather")
```

Output

```text
Hot Weather
```

---

# Condition is False

```python
age = 15

if age >= 18:
    print("Eligible for Voting")
```

Output

```text
No Output
```

Reason:

```text
Condition is False
```

---

# Understanding Step by Step

Program:

```python
age = 20

if age >= 18:
    print("Eligible")
```

---

## Step 1

```python
age >= 18
```

becomes

```python
20 >= 18
```

---

## Step 2

Result:

```text
True
```

---

## Step 3

Execute:

```python
print("Eligible")
```

Output

```text
Eligible
```

---

# 4. Indentation

Indentation means spaces before a statement.

Python uses indentation to identify code blocks.

---

# Correct Example

```python
age = 20

if age >= 18:
    print("Eligible")
```

---

# Visual Representation

```text
if condition:
    statement
```

Notice:

```text
4 spaces
```

before the print statement.

---

# Incorrect Example

```python
age = 20

if age >= 18:
print("Eligible")
```

Output

```text
IndentationError
```

---

# Why Indentation?

Other languages use:

```text
{}
```

Python uses:

```text
Indentation
```

to improve readability.

---

# Multiple Statements Inside if

```python
age = 20

if age >= 18:
    print("Eligible")
    print("Can Vote")
    print("Adult")
```

Output

```text
Eligible
Can Vote
Adult
```

---

# What Happens After if Block?

```python
age = 20

if age >= 18:
    print("Eligible")

print("Program Ended")
```

Output

```text
Eligible
Program Ended
```

---

# Example Using User Input

```python
age = int(input("Enter Age: "))

if age >= 18:
    print("Eligible for Voting")
```

---

# Sample Run

Input

```text
21
```

Output

```text
Eligible for Voting
```

---

# Example: Pass or Fail

```python
marks = int(input("Enter Marks: "))

if marks >= 35:
    print("Pass")
```

---

# Sample Run

Input

```text
80
```

Output

```text
Pass
```

---

# Example: ATM Minimum Balance

```python
balance = int(input("Enter Balance: "))

if balance >= 1000:
    print("Minimum Balance Maintained")
```

---

# Example: Driving Eligibility

```python
age = int(input("Enter Age: "))

if age >= 18:
    print("Eligible for Driving License")
```

---

# Example: Employee Bonus

```python
salary = int(input("Enter Salary: "))

if salary >= 50000:
    print("Bonus Eligible")
```

---

# Example: Movie Ticket Eligibility

```python
age = int(input("Enter Age: "))

if age >= 12:
    print("Adult Ticket")
```

---

# Using Logical Operators

```python
age = 25
salary = 60000

if age >= 18 and salary >= 50000:
    print("Loan Eligible")
```

Output

```text
Loan Eligible
```

---

# Example Using OR

```python
attendance = 80
sports = True

if attendance >= 75 or sports:
    print("Exam Eligible")
```

Output

```text
Exam Eligible
```

---

# Example Using Membership Operator

```python
subjects = ["Python", "SQL", "HTML"]

if "Python" in subjects:
    print("Subject Available")
```

Output

```text
Subject Available
```

---

# Example Using Identity Operator

```python
x = 100
y = 100

if x is y:
    print("Same Object")
```

Output

```text
Same Object
```

---

# Nested Calculations in Condition

```python
a = 10
b = 20

if a + b > 25:
    print("Greater Than 25")
```

Output

```text
Greater Than 25
```

---

# Mini Project 1

Voting Eligibility Checker

```python
age = int(input("Enter Age: "))

if age >= 18:
    print("Eligible for Voting")
```

---

# Mini Project 2

Pass Checker

```python
marks = int(input("Enter Marks: "))

if marks >= 35:
    print("Pass")
```

---

# Mini Project 3

Salary Bonus Checker

```python
salary = int(input("Enter Salary: "))

if salary >= 50000:
    print("Bonus Eligible")
```

---

# Mini Project 4

Even Number Checker

```python
num = int(input("Enter Number: "))

if num % 2 == 0:
    print("Even Number")
```

---

# Mini Project 5

Positive Number Checker

```python
num = int(input("Enter Number: "))

if num > 0:
    print("Positive Number")
```

---

# Common Mistakes

## Missing Colon

Wrong

```python
if age >= 18
    print("Eligible")
```

Correct

```python
if age >= 18:
    print("Eligible")
```

---

## Missing Indentation

Wrong

```python
if age >= 18:
print("Eligible")
```

Correct

```python
if age >= 18:
    print("Eligible")
```

---

## Using = Instead of ==

Wrong

```python
if age = 18:
```

Correct

```python
if age == 18:
```

---

# Practice Exercises

## Exercise 1

Check whether age is greater than 18.

---

## Exercise 2

Check whether marks are greater than 35.

---

## Exercise 3

Check whether salary is greater than 50000.

---

## Exercise 4

Check whether a number is even.

---

## Exercise 5

Check whether a number is positive.

---

## Exercise 6

Check whether attendance is greater than 75.

---

## Exercise 7

Check whether a student is eligible for a scholarship.

Condition:

```text
Marks >= 90
```

---

## Exercise 8

Check whether a user is allowed access.

Condition:

```text
Username exists in list
```

---

# Self Study Problems

1. Driving License Eligibility
2. Voting Eligibility
3. ATM Balance Checker
4. Loan Eligibility Checker
5. Employee Bonus Checker
6. Student Pass Checker
7. Scholarship Eligibility
8. Even Number Checker
9. Positive Number Checker
10. Subject Availability Checker

---

# Quick Summary

| Topic                | Description                     |
| -------------------- | ------------------------------- |
| Condition            | True or False Expression        |
| if                   | Executes when condition is True |
| Colon (:)            | Required after if               |
| Indentation          | Defines code block              |
| True                 | Execute Block                   |
| False                | Skip Block                      |
| Logical Operators    | Combine Conditions              |
| Membership Operators | Check Existence                 |
| Identity Operators   | Compare Objects                 |

---

# Session Summary

Today we learned:

✔ Decision Making

✔ Conditions

✔ True and False

✔ if Statement

✔ Colon Usage

✔ Indentation

✔ User Input with Conditions

✔ Logical Conditions

✔ Membership Conditions

✔ Identity Conditions

✔ Real-World Eligibility Programs

---

# Homework

1. Create Voting Eligibility Checker.
2. Create Pass/Fail Checker (only Pass using if).
3. Create Driving License Eligibility Checker.
4. Create Employee Bonus Checker.
5. Create Even Number Checker.
6. Create Positive Number Checker.
7. Practice 20 if Statement Examples.

---

# Next Session Preview

## Week 2 – Day 7

* if-else Statement
* Nested if
* Decision Making with Alternatives
* Real World Applications

Now your programs can decide what to do when a condition is True!
