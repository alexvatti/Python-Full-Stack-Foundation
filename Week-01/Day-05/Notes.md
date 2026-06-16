# Python Full Stack Foundation

# Week 1 – Day 5

## Expressions, Operator Precedence, Mini Practice Problems, Calculator Project

---

# Learning Objectives

By the end of this session, learners will be able to:

* Understand Expressions
* Understand Operators and Operands
* Learn Operator Precedence
* Evaluate Expressions Correctly
* Use Parentheses Effectively
* Solve Practice Problems
* Build a Calculator Project
* Apply Concepts Learned in Week 1

---

# Recap of Week 1

Previously we learned:

* Variables
* Data Types
* Naming Rules
* Comments
* Input and Output
* Type Casting
* Arithmetic Operators
* Assignment Operators
* Relational Operators
* Logical Operators
* Membership Operators
* Identity Operators

Today we will combine everything learned so far.

---

# 1. What is an Expression?

An Expression is a combination of:

* Values
* Variables
* Operators
* Function Calls

that produces a result.

---

## Simple Expression

```python
10 + 20
```

Output

```text
30
```

---

## Variable Expression

```python
a = 10
b = 20

result = a + b

print(result)
```

Output

```text
30
```

---

## More Examples

```python
5 * 4
```

Output

```text
20
```

---

```python
100 / 5
```

Output

```text
20.0
```

---

```python
10 > 5
```

Output

```text
True
```

---

```python
10 > 5 and 20 > 10
```

Output

```text
True
```

---

# Components of an Expression

Example:

```python
10 + 20
```

| Component | Value |
| --------- | ----- |
| Operand 1 | 10    |
| Operator  | +     |
| Operand 2 | 20    |

---

# Expression Types

| Type       | Example         |
| ---------- | --------------- |
| Arithmetic | 10 + 20         |
| Relational | 10 > 5          |
| Logical    | True and False  |
| Membership | "P" in "Python" |
| Identity   | a is b          |

---

# Arithmetic Expressions

```python
a = 10
b = 5

print(a + b)
```

Output

```text
15
```

---

```python
print(a - b)
```

Output

```text
5
```

---

```python
print(a * b)
```

Output

```text
50
```

---

```python
print(a / b)
```

Output

```text
2.0
```

---

# Relational Expressions

```python
print(20 > 10)
```

Output

```text
True
```

---

```python
print(20 == 20)
```

Output

```text
True
```

---

```python
print(20 != 10)
```

Output

```text
True
```

---

# Logical Expressions

```python
print(True and True)
```

Output

```text
True
```

---

```python
print(True and False)
```

Output

```text
False
```

---

```python
print(True or False)
```

Output

```text
True
```

---

# Membership Expressions

```python
print("P" in "Python")
```

Output

```text
True
```

---

```python
print("Z" in "Python")
```

Output

```text
False
```

---

# Identity Expressions

```python
x = 10
y = 10

print(x is y)
```

Output

```text
True
```

---

# 2. Operator Precedence

## What is Operator Precedence?

Operator Precedence decides:

```text
Which operator executes first?
```

Just like mathematics follows rules:

```text
Multiplication before Addition
Division before Subtraction
```

Python follows similar rules.

---

# Example 1

```python
print(10 + 5 * 2)
```

Output

```text
20
```

Why?

```text
5 × 2 = 10

10 + 10 = 20
```

---

# Example 2

```python
print(20 - 10 / 2)
```

Output

```text
15.0
```

Why?

```text
10 / 2 = 5

20 - 5 = 15
```

---

# Example 3

```python
print(10 + 2 * 3)
```

Output

```text
16
```

Calculation

```text
2 * 3 = 6

10 + 6 = 16
```

---

# Parentheses Have Highest Priority

```python
print((10 + 2) * 3)
```

Output

```text
36
```

Calculation

```text
10 + 2 = 12

12 * 3 = 36
```

---

# Operator Precedence Table

| Priority | Operator             |
| -------- | -------------------- |
| 1        | ()                   |
| 2        | **                   |
| 3        | *, /, //, %          |
| 4        | +, -                 |
| 5        | ==, !=, >, <, >=, <= |
| 6        | not                  |
| 7        | and                  |
| 8        | or                   |

---

# Example 4

```python
print(2 + 3 * 4)
```

Output

```text
14
```

---

# Example 5

```python
print((2 + 3) * 4)
```

Output

```text
20
```

---

# Example 6

```python
print(2 ** 3 * 2)
```

Output

```text
16
```

Calculation

```text
2 ** 3 = 8

8 * 2 = 16
```

---

# Example 7

```python
print(10 > 5 and 20 > 10)
```

Output

```text
True
```

---

# Example 8

```python
print(10 > 20 or 30 > 20)
```

Output

```text
True
```

---

# Parentheses Improve Readability

Without Parentheses

```python
print(10 + 20 * 5)
```

With Parentheses

```python
print((10 + 20) * 5)
```

Always use parentheses when calculations become complex.

---

# 3. Mini Practice Problems

---

# Problem 1

Add Two Numbers

```python
a = 10
b = 20

print(a + b)
```

Output

```text
30
```

---

# Problem 2

Find Area of Rectangle

```python
length = 10
width = 5

area = length * width

print(area)
```

Output

```text
50
```

---

# Problem 3

Find Perimeter of Rectangle

Formula

```text
2 × (Length + Width)
```

Program

```python
length = 10
width = 5

perimeter = 2 * (length + width)

print(perimeter)
```

Output

```text
30
```

---

# Problem 4

Simple Interest

Formula

```python
p = 10000
r = 8
t = 3

si = (p * r * t) / 100

print(si)
```

Output

```text
2400
```

---

# Problem 5

Average of Three Numbers

```python
a = 10
b = 20
c = 30

avg = (a + b + c) / 3

print(avg)
```

Output

```text
20.0
```

---

# Problem 6

Check Voting Eligibility

```python
age = 20

print(age >= 18)
```

Output

```text
True
```

---

# Problem 7

Check Pass or Fail

```python
marks = 70

print(marks >= 35)
```

Output

```text
True
```

---

# Problem 8

Check Number is Even

```python
num = 10

print(num % 2 == 0)
```

Output

```text
True
```

---

# Problem 9

Check Number is Odd

```python
num = 7

print(num % 2 != 0)
```

Output

```text
True
```

---

# Problem 10

Salary Hike

```python
salary = 50000
hike = 20

new_salary = salary + (salary * hike / 100)

print(new_salary)
```

Output

```text
60000
```

---

# 4. Calculator Project

## Project Requirements

The calculator should:

* Accept two numbers
* Perform Addition
* Perform Subtraction
* Perform Multiplication
* Perform Division
* Display Results

---

# Version 1 – Simple Calculator

```python
a = int(input("Enter First Number: "))
b = int(input("Enter Second Number: "))

print("Addition =", a + b)
print("Subtraction =", a - b)
print("Multiplication =", a * b)
print("Division =", a / b)
```

---

# Sample Run

Input

```text
10
5
```

Output

```text
Addition = 15
Subtraction = 5
Multiplication = 50
Division = 2.0
```

---

# Version 2 – Using Variables

```python
a = int(input("Enter First Number: "))
b = int(input("Enter Second Number: "))

add = a + b
sub = a - b
mul = a * b
div = a / b

print(add)
print(sub)
print(mul)
print(div)
```

---

# Version 3 – Using f-Strings

```python
a = int(input("Enter First Number: "))
b = int(input("Enter Second Number: "))

print(f"Addition = {a+b}")
print(f"Subtraction = {a-b}")
print(f"Multiplication = {a*b}")
print(f"Division = {a/b}")
```

---

# Version 4 – Menu Driven Calculator

```python
print("1. Addition")
print("2. Subtraction")
print("3. Multiplication")
print("4. Division")

choice = int(input("Enter Choice: "))

a = int(input("Enter First Number: "))
b = int(input("Enter Second Number: "))

if choice == 1:
    print(a + b)

if choice == 2:
    print(a - b)

if choice == 3:
    print(a * b)

if choice == 4:
    print(a / b)
```

Note:

We will improve this version after learning Conditions and Loops.

---

# Self Study Problems

## Problem 1

Calculate Area of Square

---

## Problem 2

Calculate Area of Circle

---

## Problem 3

Calculate GST Amount

---

## Problem 4

Calculate Discount Amount

---

## Problem 5

Calculate Attendance Percentage

---

## Problem 6

Calculate Student Average Marks

---

## Problem 7

Calculate Electricity Bill

---

## Problem 8

Calculate Monthly EMI Interest

---

## Problem 9

Calculate Employee Bonus

---

## Problem 10

Calculate Profit or Loss

---

# Quick Summary

| Topic                 | Description                         |
| --------------------- | ----------------------------------- |
| Expression            | Combination of values and operators |
| Arithmetic Expression | Mathematical calculation            |
| Relational Expression | Comparison                          |
| Logical Expression    | Multiple conditions                 |
| Membership Expression | Search value                        |
| Identity Expression   | Compare objects                     |
| Precedence            | Order of execution                  |
| Parentheses           | Highest priority                    |
| Calculator            | Practical application               |

---

# Session Summary

Today we learned:

✔ Expressions

✔ Operands and Operators

✔ Arithmetic Expressions

✔ Relational Expressions

✔ Logical Expressions

✔ Membership Expressions

✔ Identity Expressions

✔ Operator Precedence

✔ Parentheses

✔ Practice Problems

✔ Calculator Project

---

# Homework

1. Create a Simple Calculator.
2. Create a GST Calculator.
3. Create a Salary Hike Calculator.
4. Create an Attendance Percentage Calculator.
5. Create a Student Average Calculator.
6. Solve 10 Operator Precedence Examples.
7. Create 10 Arithmetic Expressions.
8. Create 10 Logical Expressions.

---

# Week 1 Completed 🎉

You can now:

✔ Take Input

✔ Store Data

✔ Display Output

✔ Perform Calculations

✔ Compare Values

✔ Use Operators

✔ Build Basic Python Programs

---

# Next Session Preview

## Week 2 – Day 6

* if Statement
* Conditions
* Indentation
* Decision Making in Python

Get ready to make programs think and take decisions!
