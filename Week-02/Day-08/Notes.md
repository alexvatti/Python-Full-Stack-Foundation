# Python Full Stack Foundation

# Week 2 – Day 8

## if-elif-else Statement, Multiple Conditions

---

# Learning Objectives

By the end of this session, learners will be able to:

* Understand `if-elif-else`
* Handle Multiple Conditions
* Build Grade Systems
* Create Menu-Driven Programs
* Solve Real-World Decision-Making Problems
* Understand Flow of Control

---

# Recap

Previously we learned:

* if Statement
* if-else Statement
* Nested if

---

# Limitation of if-else

Suppose we want to assign grades.

```text
Marks >= 90  → A Grade
Marks >= 75  → B Grade
Marks >= 60  → C Grade
Marks >= 35  → Pass
Marks < 35   → Fail
```

Using only if-else becomes difficult.

Solution:

```text
if-elif-else
```

---

# 1. What is if-elif-else?

Used when there are multiple conditions.

Python checks conditions one by one.

As soon as one condition becomes True:

```text
Remaining conditions are skipped.
```

---

# Syntax

```python
if condition1:
    statements

elif condition2:
    statements

elif condition3:
    statements

else:
    statements
```

---

# Flow Diagram

```text
Condition 1
      |
   True?
   /   \
 Yes    No
 |       |
Block1  Condition2
           |
        True?
        /   \
      Yes   No
       |      |
    Block2  Condition3
                |
             True?
             /   \
           Yes   No
            |      |
         Block3  Else Block
```

---

# Example 1

```python
marks = 95

if marks >= 90:
    print("A Grade")

elif marks >= 75:
    print("B Grade")

elif marks >= 60:
    print("C Grade")

else:
    print("Fail")
```

Output

```text
A Grade
```

---

# Step-by-Step Execution

```python
marks = 95
```

Check:

```python
marks >= 90
```

Result:

```text
True
```

Execute:

```python
print("A Grade")
```

Stop checking remaining conditions.

---

# Example 2

```python
marks = 80

if marks >= 90:
    print("A Grade")

elif marks >= 75:
    print("B Grade")

elif marks >= 60:
    print("C Grade")

else:
    print("Fail")
```

Output

```text
B Grade
```

---

# Example 3

```python
marks = 65

if marks >= 90:
    print("A Grade")

elif marks >= 75:
    print("B Grade")

elif marks >= 60:
    print("C Grade")

else:
    print("Fail")
```

Output

```text
C Grade
```

---

# Example 4

```python
marks = 20

if marks >= 90:
    print("A Grade")

elif marks >= 75:
    print("B Grade")

elif marks >= 60:
    print("C Grade")

else:
    print("Fail")
```

Output

```text
Fail
```

---

# Important Rule

Only one block executes.

---

# Example

```python
number = 50

if number > 100:
    print("A")

elif number > 40:
    print("B")

elif number > 20:
    print("C")

else:
    print("D")
```

Output

```text
B
```

Even though:

```python
number > 20
```

is also True,

Python stops after finding the first True condition.

---

# Grade Calculator

```python
marks = int(input("Enter Marks: "))

if marks >= 90:
    print("Grade A")

elif marks >= 75:
    print("Grade B")

elif marks >= 60:
    print("Grade C")

elif marks >= 35:
    print("Pass")

else:
    print("Fail")
```

---

# Sample Run

Input

```text
82
```

Output

```text
Grade B
```

---

# 2. Multiple Conditions

Multiple conditions are created using:

* and
* or
* not

---

# AND Operator

Both conditions must be True.

```python
age = 25
salary = 60000

if age >= 21 and salary >= 50000:
    print("Loan Eligible")
```

Output

```text
Loan Eligible
```

---

# Example

```python
username = "admin"
password = "1234"

if username == "admin" and password == "1234":
    print("Login Successful")
```

Output

```text
Login Successful
```

---

# OR Operator

At least one condition must be True.

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

# Example

```python
day = "Sunday"

if day == "Saturday" or day == "Sunday":
    print("Holiday")
```

Output

```text
Holiday"
```

---

# NOT Operator

Reverses the result.

```python
logged_in = False

if not logged_in:
    print("Please Login")
```

Output

```text
Please Login
```

---

# Example – Driving License

```python
age = int(input("Enter Age: "))

if age >= 18:
    print("Eligible")

else:
    print("Not Eligible")
```

---

# Example – Scholarship

```python
marks = int(input("Enter Marks: "))

if marks >= 90:
    print("Scholarship Approved")

elif marks >= 75:
    print("Merit Category")

else:
    print("Not Eligible")
```

---

# Example – Employee Bonus

```python
salary = int(input("Enter Salary: "))

if salary >= 100000:
    print("Bonus 20%")

elif salary >= 50000:
    print("Bonus 10%")

elif salary >= 30000:
    print("Bonus 5%")

else:
    print("No Bonus")
```

---

# Example – Electricity Bill Category

```python
units = int(input("Enter Units: "))

if units <= 100:
    print("Low Usage")

elif units <= 300:
    print("Medium Usage")

else:
    print("High Usage")
```

---

# Example – Ticket Pricing

```python
age = int(input("Enter Age: "))

if age < 5:
    print("Free Ticket")

elif age <= 18:
    print("Child Ticket")

elif age <= 60:
    print("Adult Ticket")

else:
    print("Senior Citizen Ticket")
```

---

# Example – Largest of Three Numbers

```python
a = 50
b = 80
c = 60

if a >= b and a >= c:
    print("A is Largest")

elif b >= a and b >= c:
    print("B is Largest")

else:
    print("C is Largest")
```

Output

```text
B is Largest
```

---

# Example – ATM Menu

```python
choice = int(input("Enter Choice: "))

if choice == 1:
    print("Balance")

elif choice == 2:
    print("Deposit")

elif choice == 3:
    print("Withdraw")

else:
    print("Invalid Choice")
```

---

# Menu Driven Example

```python
print("1. Addition")
print("2. Subtraction")
print("3. Multiplication")
print("4. Division")

choice = int(input("Enter Choice: "))

if choice == 1:
    print("Addition Selected")

elif choice == 2:
    print("Subtraction Selected")

elif choice == 3:
    print("Multiplication Selected")

elif choice == 4:
    print("Division Selected")

else:
    print("Invalid Choice")
```

---

# Nested if vs if-elif-else

| Nested if                                 | if-elif-else                             |
| ----------------------------------------- | ---------------------------------------- |
| Multiple levels                           | Multiple choices                         |
| Complex                                   | Simpler                                  |
| Used when conditions depend on each other | Used when only one option should execute |

---

# Common Mistakes

## Wrong Order

Wrong

```python
marks = 90

if marks >= 35:
    print("Pass")

elif marks >= 90:
    print("A Grade")
```

Output

```text
Pass
```

Reason:

```text
First condition becomes True.
```

---

# Correct Order

```python
if marks >= 90:
    print("A Grade")

elif marks >= 75:
    print("B Grade")

elif marks >= 35:
    print("Pass")

else:
    print("Fail")
```

---

# Practice Exercises

## Exercise 1

Create Grade Calculator.

---

## Exercise 2

Create Employee Bonus Calculator.

---

## Exercise 3

Create Ticket Pricing System.

---

## Exercise 4

Create Largest of Three Numbers Program.

---

## Exercise 5

Create Login Validation Program.

---

## Exercise 6

Create Loan Eligibility Program.

Condition:

```text
Age >= 21
Salary >= 50000
```

---

## Exercise 7

Create ATM Menu.

---

## Exercise 8

Create Scholarship Program.

---

## Exercise 9

Create Electricity Bill Category Program.

---

## Exercise 10

Create Student Result System.

---

# Mini Project 1

Student Grade System

```python
marks = int(input("Enter Marks: "))

if marks >= 90:
    print("A Grade")

elif marks >= 75:
    print("B Grade")

elif marks >= 60:
    print("C Grade")

elif marks >= 35:
    print("Pass")

else:
    print("Fail")
```

---

# Mini Project 2

Bonus Calculator

```python
salary = int(input("Enter Salary: "))

if salary >= 100000:
    print("20% Bonus")

elif salary >= 50000:
    print("10% Bonus")

else:
    print("No Bonus")
```

---

# Quick Summary

| Topic               | Description             |
| ------------------- | ----------------------- |
| if                  | First Condition         |
| elif                | Additional Conditions   |
| else                | Default Block           |
| and                 | Both True               |
| or                  | Any One True            |
| not                 | Reverse Result          |
| Multiple Conditions | Complex Decision Making |

---

# Session Summary

Today we learned:

✔ if-elif-else

✔ Multiple Conditions

✔ Grade Systems

✔ Loan Eligibility

✔ Login Validation

✔ Employee Bonus Programs

✔ ATM Menus

✔ Largest Number Logic

✔ Real-World Decision Making

---

# Homework

1. Create Grade Calculator.
2. Create Salary Bonus Calculator.
3. Create Scholarship Checker.
4. Create Ticket Pricing Program.
5. Create ATM Menu Program.
6. Create Largest of Three Numbers Program.
7. Practice 20 if-elif-else Programs.
8. Practice 10 Programs Using AND/OR.

---

# Next Session Preview

## Week 2 – Day 9

* for Loop
* range()
* Loop Patterns
* Repeating Tasks
* Iteration Concepts

Get ready to automate repetitive tasks using loops!
