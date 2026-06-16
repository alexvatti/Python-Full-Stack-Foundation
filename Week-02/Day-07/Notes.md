# Python Full Stack Foundation

# Week 2 – Day 7

## if-else Statement, Nested if

---

# Learning Objectives

By the end of this session, learners will be able to:

* Understand the `if-else` Statement
* Execute Alternative Actions
* Understand Nested if
* Make Multi-Level Decisions
* Build Real-World Decision Programs
* Solve Eligibility and Validation Problems

---

# Recap of Day 6

Previously we learned:

* Conditions
* True and False
* if Statement
* Indentation
* Decision Making

### Limitation of if Statement

```python
age = 15

if age >= 18:
    print("Eligible for Voting")
```

Output

```text
No Output
```

Problem:

```text
What if we want to display
"Not Eligible" ?
```

Solution:

```text
if-else Statement
```

---

# 1. What is if-else?

The `if-else` statement executes:

* One block when condition is True
* Another block when condition is False

---

# Syntax

```python
if condition:
    statements
else:
    statements
```

---

# Flow Diagram

```text
            Condition
                |
         ----------------
         |              |
       True          False
         |              |
     if Block      else Block
```

---

# Example 1

```python
age = 20

if age >= 18:
    print("Eligible for Voting")
else:
    print("Not Eligible")
```

Output

```text
Eligible for Voting
```

---

# Example 2

```python
age = 15

if age >= 18:
    print("Eligible for Voting")
else:
    print("Not Eligible")
```

Output

```text
Not Eligible
```

---

# Step-by-Step Execution

```python
age = 15

if age >= 18:
    print("Eligible")
else:
    print("Not Eligible")
```

### Step 1

```python
15 >= 18
```

Result

```text
False
```

### Step 2

Skip if block

### Step 3

Execute else block

Output

```text
Not Eligible
```

---

# Example 3 – Pass or Fail

```python
marks = 75

if marks >= 35:
    print("Pass")
else:
    print("Fail")
```

Output

```text
Pass
```

---

# Example 4 – Even or Odd

```python
num = 10

if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

Output

```text
Even
```

---

# Example 5 – Positive or Negative

```python
num = -5

if num > 0:
    print("Positive")
else:
    print("Negative")
```

Output

```text
Negative
```

---

# Example 6 – Largest of Two Numbers

```python
a = 10
b = 20

if a > b:
    print("A is Larger")
else:
    print("B is Larger")
```

Output

```text
B is Larger
```

---

# Using User Input

## Voting Eligibility

```python
age = int(input("Enter Age: "))

if age >= 18:
    print("Eligible for Voting")
else:
    print("Not Eligible")
```

---

# Sample Run

Input

```text
16
```

Output

```text
Not Eligible
```

---

# Example – ATM Withdrawal

```python
balance = 5000
withdraw = 2000

if withdraw <= balance:
    print("Transaction Successful")
else:
    print("Insufficient Balance")
```

Output

```text
Transaction Successful
```

---

# Example – Scholarship Eligibility

```python
marks = 92

if marks >= 90:
    print("Scholarship Eligible")
else:
    print("Scholarship Not Eligible")
```

Output

```text
Scholarship Eligible
```

---

# Example – Login Validation

```python
password = "admin123"

if password == "admin123":
    print("Login Successful")
else:
    print("Invalid Password")
```

Output

```text
Login Successful
```

---

# Example – Divisible by 5

```python
num = 25

if num % 5 == 0:
    print("Divisible by 5")
else:
    print("Not Divisible by 5")
```

Output

```text
Divisible by 5
```

---

# Example – Adult or Child

```python
age = 12

if age >= 18:
    print("Adult")
else:
    print("Child")
```

Output

```text
Child
```

---

# 2. Nested if

---

# What is Nested if?

A Nested if means:

```text
An if statement inside another if statement.
```

---

# Syntax

```python
if condition1:

    if condition2:
        statements
```

---

# Flow

```text
Condition 1
      |
    True
      |
Condition 2
      |
    True
      |
 Execute
```

---

# Example 1

```python
age = 25

if age >= 18:

    if age <= 60:
        print("Working Age Group")
```

Output

```text
Working Age Group
```

---

# Step-by-Step

### Outer Condition

```python
25 >= 18
```

Result

```text
True
```

Move inside.

### Inner Condition

```python
25 <= 60
```

Result

```text
True
```

Execute.

---

# Example 2 – Exam Eligibility

```python
attendance = 80

if attendance >= 75:

    if attendance <= 100:
        print("Eligible for Exam")
```

Output

```text
Eligible for Exam
```

---

# Example 3 – Loan Eligibility

```python
age = 30
salary = 60000

if age >= 21:

    if salary >= 50000:
        print("Loan Eligible")
```

Output

```text
Loan Eligible
```

---

# Example 4 – Employee Bonus

```python
experience = 5
salary = 70000

if experience >= 3:

    if salary >= 50000:
        print("Bonus Eligible")
```

Output

```text
Bonus Eligible
```

---

# Nested if with else

```python
age = 16

if age >= 18:

    if age >= 21:
        print("Can Apply for Certain Licenses")
    else:
        print("Adult but Restricted")

else:
    print("Minor")
```

Output

```text
Minor
```

---

# Example – College Admission

```python
marks = 85

if marks >= 60:

    if marks >= 80:
        print("Admission Confirmed")
    else:
        print("Waiting List")

else:
    print("Not Eligible")
```

Output

```text
Admission Confirmed
```

---

# Example – Bank Account Opening

```python
age = 22
documents = True

if age >= 18:

    if documents:
        print("Account Can Be Opened")
    else:
        print("Documents Required")

else:
    print("Age Requirement Not Met")
```

Output

```text
Account Can Be Opened
```

---

# Difference Between if and if-else

| if                      | if-else                     |
| ----------------------- | --------------------------- |
| Executes only when True | Handles both True and False |
| May produce no output   | Always one block executes   |
| Simple decisions        | Complete decisions          |

---

# Difference Between if-else and Nested if

| if-else       | Nested if            |
| ------------- | -------------------- |
| One condition | Multiple conditions  |
| Two outcomes  | Multi-level checking |
| Simpler logic | More detailed logic  |

---

# Mini Project 1

Voting Eligibility

```python
age = int(input("Enter Age: "))

if age >= 18:
    print("Eligible")
else:
    print("Not Eligible")
```

---

# Mini Project 2

Even or Odd

```python
num = int(input("Enter Number: "))

if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

---

# Mini Project 3

Loan Eligibility

```python
age = int(input("Enter Age: "))
salary = int(input("Enter Salary: "))

if age >= 21:

    if salary >= 50000:
        print("Loan Eligible")
    else:
        print("Salary Requirement Not Met")

else:
    print("Age Requirement Not Met")
```

---

# Mini Project 4

Login System

```python
username = input("Enter Username: ")

if username == "admin":
    print("Access Granted")
else:
    print("Access Denied")
```

---

# Mini Project 5

Student Pass/Fail

```python
marks = int(input("Enter Marks: "))

if marks >= 35:
    print("Pass")
else:
    print("Fail")
```

---

# Common Mistakes

## Missing Colon

Wrong

```python
if age >= 18
```

Correct

```python
if age >= 18:
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

## Wrong Equality Operator

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

Check whether a person is eligible for voting.

---

## Exercise 2

Check whether a number is even or odd.

---

## Exercise 3

Check whether a number is positive or negative.

---

## Exercise 4

Find larger of two numbers.

---

## Exercise 5

Check whether marks indicate Pass or Fail.

---

## Exercise 6

Check whether salary qualifies for bonus.

---

## Exercise 7

Create a Login Validation Program.

---

## Exercise 8

Create a Loan Eligibility Program using Nested if.

---

## Exercise 9

Create a Scholarship Eligibility Program.

---

## Exercise 10

Create an ATM Withdrawal Validation Program.

---

# Self Study Problems

1. Driving License Eligibility
2. Movie Ticket Validation
3. Railway Ticket Category
4. Employee Bonus Checker
5. College Admission Checker
6. Scholarship Checker
7. Loan Eligibility Checker
8. Account Opening Validation
9. Student Pass/Fail
10. Login Validation

---

# Quick Summary

| Topic       | Description                      |
| ----------- | -------------------------------- |
| if          | Executes when condition is True  |
| else        | Executes when condition is False |
| if-else     | Two-way decision                 |
| Nested if   | if inside another if             |
| Condition   | True/False Expression            |
| Indentation | Defines Block                    |
| ==          | Equality Check                   |

---

# Session Summary

Today we learned:

✔ if-else Statement

✔ Alternative Execution

✔ Nested if

✔ Multi-Level Decisions

✔ Login Validation

✔ Loan Eligibility

✔ Pass/Fail Programs

✔ ATM Validation

✔ Real-World Decision Making

---

# Homework

1. Create Voting Eligibility Program.
2. Create Even/Odd Program.
3. Create Largest of Two Numbers Program.
4. Create Pass/Fail Program.
5. Create Login Validation Program.
6. Create Loan Eligibility Program using Nested if.
7. Practice 20 if-else Programs.
8. Practice 10 Nested if Programs.

---

# Next Session Preview

## Week 2 – Day 8

* if-elif-else Statement
* Multiple Conditions
* Grade System
* Menu Driven Programs
* Real World Decision Making

Get ready to handle multiple choices and outcomes in Python!
