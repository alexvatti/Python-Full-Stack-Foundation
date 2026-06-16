# Python Full Stack Foundation

# Week 1 – Day 2

## Variables, Data Types, Naming Rules, Comments, Input(), Output()

---

# Learning Objectives

By the end of this session, learners will be able to:

* Understand Variables
* Store and retrieve data
* Identify Python Data Types
* Follow Variable Naming Rules
* Write Comments
* Take User Input
* Display Output
* Build simple interactive programs

---

# Recap of Day 1

Previously we learned:

* What is Programming
* Why Python
* Problem Solving Approach
* Python Installation
* VS Code Setup
* First Python Program
* print() Function

Today we will make our programs interactive.

---

# 1. Variables

## What is a Variable?

A variable is a container used to store data.

Think of it as a labeled box.

Example:

```text
Name Box   → Alex
Age Box    → 25
City Box   → Hyderabad
```

In Python:

```python
name = "Alex"
age = 25
city = "Hyderabad"
```

---

# Why Variables?

Without Variables

```python
print("Alex")
print(25)
print("Hyderabad")
```

With Variables

```python
name = "Alex"
age = 25
city = "Hyderabad"

print(name)
print(age)
print(city)
```

Variables make programs reusable.

---

# Variable Creation

Syntax

```python
variable_name = value
```

Examples

```python
name = "Alex"
age = 25
salary = 50000
```

---

# Accessing Variables

```python
name = "Alex"

print(name)
```

Output

```text
Alex
```

---

# Updating Variables

```python
age = 25

print(age)

age = 26

print(age)
```

Output

```text
25
26
```

---

# Multiple Variables

```python
name = "Alex"
age = 25
city = "Hyderabad"

print(name)
print(age)
print(city)
```

---

# Multiple Assignment

```python
a, b, c = 10, 20, 30

print(a)
print(b)
print(c)
```

Output

```text
10
20
30
```

---

# Same Value Assignment

```python
x = y = z = 100

print(x)
print(y)
print(z)
```

Output

```text
100
100
100
```

---

# 2. Data Types

## What is a Data Type?

A Data Type tells Python what kind of data is stored.

Examples:

* Text
* Number
* Decimal Number
* True/False

---

# Common Data Types

| Data Type | Example |
| --------- | ------- |
| str       | "Alex"  |
| int       | 25      |
| float     | 99.99   |
| bool      | True    |

---

# String (str)

Stores text.

```python
name = "Alex"

print(name)
```

Output

```text
Alex
```

---

# Integer (int)

Stores whole numbers.

```python
age = 25

print(age)
```

Output

```text
25
```

---

# Float

Stores decimal values.

```python
percentage = 89.75

print(percentage)
```

Output

```text
89.75
```

---

# Boolean

Stores True or False.

```python
is_student = True

print(is_student)
```

Output

```text
True
```

---

# Finding Data Type

Use:

```python
type()
```

Example

```python
name = "Alex"

print(type(name))
```

Output

```text
<class 'str'>
```

---

# More Examples

```python
print(type("Python"))
print(type(100))
print(type(99.99))
print(type(True))
```

Output

```text
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

---

# 3. Variable Naming Rules

A variable name should be meaningful.

Good Example

```python
student_name = "Alex"
student_age = 25
```

Bad Example

```python
a = "Alex"
b = 25
```

---

# Rules

## Rule 1

Must start with:

* Letter
* Underscore (_)

Valid

```python
name = "Alex"
_age = 25
```

Invalid

```python
1name = "Alex"
```

---

## Rule 2

Cannot contain spaces

Invalid

```python
student name = "Alex"
```

Valid

```python
student_name = "Alex"
```

---

## Rule 3

Can contain

* Letters
* Numbers
* Underscores

Valid

```python
student1 = "Alex"
student_name = "Alex"
```

---

## Rule 4

Case Sensitive

```python
name = "Alex"
Name = "John"
```

These are different variables.

---

## Rule 5

Cannot use Keywords

Invalid

```python
if = 10
for = 20
```

Python reserves these words.

---

# Naming Conventions

Preferred Style:

```python
student_name
employee_salary
course_fee
```

This style is called:

```text
snake_case
```

---

# 4. Comments

Comments are notes for programmers.

Python ignores comments during execution.

---

# Single Line Comment

```python
# This is a comment

print("Python")
```

Output

```text
Python
```

---

# Why Use Comments?

* Explain code
* Improve readability
* Help other developers
* Easier maintenance

---

# Example

```python
# Student Information

name = "Alex"
age = 25

print(name)
print(age)
```

---

# Multi-Line Comments

```python
"""
Student Information Program
Created for Training
Day 2 Session
"""
```

---

# 5. Input Function

Until now we manually assigned values.

Example

```python
name = "Alex"

print(name)
```

What if the user wants to enter the value?

Use:

```python
input()
```

---

# Syntax

```python
input("Message")
```

---

# Example 1

```python
name = input("Enter Name: ")

print(name)
```

Input

```text
Alex
```

Output

```text
Alex
```

---

# Example 2

```python
city = input("Enter City: ")

print(city)
```

Input

```text
Hyderabad
```

Output

```text
Hyderabad
```

---

# Understanding Input

```python
name = input("Enter Name: ")
```

Steps:

1. Display message
2. Wait for user input
3. Store input in variable

---

# Important Point

Input always returns String.

```python
age = input("Enter Age: ")

print(type(age))
```

Output

```text
<class 'str'>
```

---

# Converting Input

## String to Integer

```python
age = int(input("Enter Age: "))

print(age)
```

---

## String to Float

```python
salary = float(input("Enter Salary: "))

print(salary)
```

---

# Example Program

```python
name = input("Enter Name: ")
age = int(input("Enter Age: "))

print(name)
print(age)
```

---

# 6. Output Function

Output means displaying information.

Python uses:

```python
print()
```

---

# Simple Output

```python
name = "Alex"

print(name)
```

Output

```text
Alex
```

---

# Output with Labels

```python
name = "Alex"

print("Name:", name)
```

Output

```text
Name: Alex
```

---

# String Concatenation

```python
name = "Alex"

print("Name: " + name)
```

Output

```text
Name: Alex
```

---

# format() Method

```python
name = "Alex"
age = 25

print("Name: {} Age: {}".format(name, age))
```

Output

```text
Name: Alex Age: 25
```

---

# f-String Method

Recommended

```python
name = "Alex"
age = 25

print(f"Name: {name}")
print(f"Age: {age}")
```

Output

```text
Name: Alex
Age: 25
```

---

# Complete Example

```python
name = input("Enter Name: ")
age = int(input("Enter Age: "))

print(f"Name: {name}")
print(f"Age: {age}")
```

---

# Mini Project 1

Student Information System

```python
name = input("Enter Name: ")
age = int(input("Enter Age: "))
city = input("Enter City: ")

print("----- Student Information -----")
print(f"Name : {name}")
print(f"Age  : {age}")
print(f"City : {city}")
```

---

# Mini Project 2

Simple Interest Input Program

```python
p = float(input("Enter Principal: "))
r = float(input("Enter Rate: "))
t = float(input("Enter Time: "))

si = (p * r * t) / 100

print(f"Simple Interest = {si}")
```

---

# Practice Exercises

## Exercise 1

Take Name as input and display it.

---

## Exercise 2

Take City as input and display it.

---

## Exercise 3

Take Age as input and display it.

---

## Exercise 4

Take Name and Age and display using f-string.

---

## Exercise 5

Take Principal, Rate and Time and display Simple Interest.

---

## Exercise 6

Take Length and Width and display Area of Rectangle.

---

# Quick Summary

| Topic    | Description       |
| -------- | ----------------- |
| Variable | Stores data       |
| String   | Text data         |
| Integer  | Whole numbers     |
| Float    | Decimal numbers   |
| Boolean  | True / False      |
| type()   | Finds data type   |
| Comment  | Notes in code     |
| input()  | Takes user input  |
| print()  | Displays output   |
| format() | String formatting |
| f-string | Modern formatting |

---

# Session Summary

Today we learned:

✔ Variables

✔ Data Types

✔ Variable Naming Rules

✔ Comments

✔ Input Function

✔ Output Function

✔ String Formatting

✔ format()

✔ f-Strings

✔ Interactive Programs

---

# Homework

1. Create a Student Information Program.
2. Create an Employee Information Program.
3. Take Name, Age, City as input.
4. Display output using:

   * print()
   * Concatenation
   * format()
   * f-string
5. Find the data type of:

   * Name
   * Age
   * Salary
   * True

---

# Next Session Preview

## Week 1 – Day 3

* Type Casting
* Arithmetic Operators
* Assignment Operators
* Mini Calculator Program

Get ready to perform calculations using Python!
