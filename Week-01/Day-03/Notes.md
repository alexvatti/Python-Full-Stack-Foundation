# Python Full Stack Foundation

# Week 1 – Day 3

## Type Casting, Arithmetic Operators, Assignment Operators

---

# Learning Objectives

By the end of this session, learners will be able to:

* Understand Type Casting
* Convert data between different data types
* Perform arithmetic calculations
* Use Arithmetic Operators
* Use Assignment Operators
* Build simple calculator programs
* Solve real-world mathematical problems using Python

---

# Recap of Day 2

Previously we learned:

* Variables
* Data Types
* Naming Rules
* Comments
* Input Function
* Output Function
* String Formatting

Today we will learn how to perform calculations in Python.

---

# 1. Type Casting

## What is Type Casting?

Type Casting means converting data from one type to another.

### Examples

| From    | To      |
| ------- | ------- |
| String  | Integer |
| String  | Float   |
| Integer | Float   |
| Float   | Integer |

---

# Why Type Casting?

Input always returns String.

Example:

```python
age = input("Enter Age: ")

print(type(age))
```

Output

```text
<class 'str'>
```

If we want mathematical calculations, we must convert it.

---

# int() Function

Converts data to Integer.

```python
age = int("25")

print(age)
print(type(age))
```

Output

```text
25
<class 'int'>
```

---

# float() Function

Converts data to Float.

```python
salary = float("25000")

print(salary)
print(type(salary))
```

Output

```text
25000.0
<class 'float'>
```

---

# str() Function

Converts data to String.

```python
age = 25

print(str(age))
print(type(str(age)))
```

Output

```text
25
<class 'str'>
```

---

# bool() Function

Converts data to Boolean.

```python
print(bool(1))
print(bool(0))
```

Output

```text
True
False
```

---

# Type Casting Examples

## String to Integer

```python
num = int("100")

print(num)
```

Output

```text
100
```

---

## String to Float

```python
price = float("99.99")

print(price)
```

Output

```text
99.99
```

---

## Integer to Float

```python
num = 100

print(float(num))
```

Output

```text
100.0
```

---

## Float to Integer

```python
num = 99.99

print(int(num))
```

Output

```text
99
```

Note:

Decimal portion is removed.

---

# Practical Example

```python
age = int(input("Enter Age: "))

print(age)
print(type(age))
```

Input

```text
25
```

Output

```text
25
<class 'int'>
```

---

# Mini Activity

Take two numbers from the user and display their sum.

```python
a = int(input("Enter First Number: "))
b = int(input("Enter Second Number: "))

print(a + b)
```

---

# 2. Arithmetic Operators

Arithmetic Operators perform mathematical operations.

---

# Arithmetic Operator Table

| Operator | Meaning        |
| -------- | -------------- |
| +        | Addition       |
| -        | Subtraction    |
| *        | Multiplication |
| /        | Division       |
| //       | Floor Division |
| %        | Modulus        |
| **       | Exponent       |

---

# Addition (+)

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

# Subtraction (-)

```python
a = 20
b = 10

print(a - b)
```

Output

```text
10
```

---

# Multiplication (*)

```python
a = 10
b = 5

print(a * b)
```

Output

```text
50
```

---

# Division (/)

```python
a = 10
b = 2

print(a / b)
```

Output

```text
5.0
```

Division always returns Float.

---

# Floor Division (//)

```python
a = 10
b = 3

print(a // b)
```

Output

```text
3
```

Only integer part is returned.

---

# Modulus (%)

Returns remainder.

```python
a = 10
b = 3

print(a % b)
```

Output

```text
1
```

---

# Exponent (**)

Power operator.

```python
print(2 ** 3)
```

Output

```text
8
```

Meaning:

```text
2 × 2 × 2
```

---

# Arithmetic Example

```python
a = 20
b = 10

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a // b)
print(a % b)
print(a ** b)
```

---

# Real World Examples

## Rectangle Area

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

## Simple Interest

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

## GST Calculation

```python
price = 1000
gst = 18

gst_amount = (price * gst) / 100

print(gst_amount)
```

Output

```text
180
```

---

## Salary Hike

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

# Operator Precedence

Python follows mathematical rules.

## Example

```python
print(10 + 5 * 2)
```

Output

```text
20
```

Multiplication happens first.

---

## Using Brackets

```python
print((10 + 5) * 2)
```

Output

```text
30
```

---

# 3. Assignment Operators

Assignment Operators assign values to variables.

---

# Basic Assignment

```python
x = 10
```

Meaning:

Store 10 in x.

---

# Assignment Operator Table

| Operator | Example |
| -------- | ------- |
| =        | x = 10  |
| +=       | x += 5  |
| -=       | x -= 5  |
| *=       | x *= 5  |
| /=       | x /= 5  |
| //=      | x //= 5 |
| %=       | x %= 5  |
| **=      | x **= 5 |

---

# += Operator

```python
x = 10

x += 5

print(x)
```

Output

```text
15
```

Equivalent to:

```python
x = x + 5
```

---

# -= Operator

```python
x = 10

x -= 3

print(x)
```

Output

```text
7
```

---

# *= Operator

```python
x = 10

x *= 2

print(x)
```

Output

```text
20
```

---

# /= Operator

```python
x = 10

x /= 2

print(x)
```

Output

```text
5.0
```

---

# %= Operator

```python
x = 10

x %= 3

print(x)
```

Output

```text
1
```

---

# **= Operator

```python
x = 2

x **= 3

print(x)
```

Output

```text
8
```

---

# Practical Assignment Example

```python
balance = 1000

balance += 500

print(balance)
```

Output

```text
1500
```

---

# Mini Project 1

Simple Calculator

```python
a = int(input("Enter First Number: "))
b = int(input("Enter Second Number: "))

print("Addition =", a + b)
print("Subtraction =", a - b)
print("Multiplication =", a * b)
print("Division =", a / b)
```

---

# Mini Project 2

Student Percentage

```python
m1 = int(input("Enter Marks 1: "))
m2 = int(input("Enter Marks 2: "))
m3 = int(input("Enter Marks 3: "))

total = m1 + m2 + m3
average = total / 3

print("Total =", total)
print("Average =", average)
```

---

# Mini Project 3

EMI Style Interest Calculator

```python
principal = float(input("Enter Principal: "))
rate = float(input("Enter Rate: "))
time = float(input("Enter Time: "))

interest = (principal * rate * time) / 100

print("Interest =", interest)
```

---

# Practice Exercises

## Exercise 1

Take two numbers and display:

* Addition
* Subtraction
* Multiplication
* Division

---

## Exercise 2

Take Length and Width and calculate Area.

---

## Exercise 3

Take Principal, Rate and Time and calculate Simple Interest.

---

## Exercise 4

Take Salary and Hike Percentage and calculate New Salary.

---

## Exercise 5

Take GST Percentage and Product Price and calculate GST Amount.

---

## Exercise 6

Use all Assignment Operators.

```python
+=
-=
*=
/=
%=
**=
```

---

# Quick Summary

| Topic   | Description         |
| ------- | ------------------- |
| int()   | Convert to Integer  |
| float() | Convert to Float    |
| str()   | Convert to String   |
| bool()  | Convert to Boolean  |
| +       | Addition            |
| -       | Subtraction         |
| *       | Multiplication      |
| /       | Division            |
| //      | Floor Division      |
| %       | Modulus             |
| **      | Exponent            |
| +=      | Add and Assign      |
| -=      | Subtract and Assign |
| *=      | Multiply and Assign |

---

# Session Summary

Today we learned:

✔ Type Casting

✔ int()

✔ float()

✔ str()

✔ bool()

✔ Arithmetic Operators

✔ Addition

✔ Subtraction

✔ Multiplication

✔ Division

✔ Modulus

✔ Exponent

✔ Assignment Operators

✔ Calculator Programs

✔ Real World Calculations

---

# Homework

1. Build a Calculator Program.
2. Build a Simple Interest Calculator.
3. Build a GST Calculator.
4. Build a Salary Hike Calculator.
5. Practice all Arithmetic Operators.
6. Practice all Assignment Operators.
7. Create 10 examples of Type Casting.

---

# Next Session Preview

## Week 1 – Day 4

* Relational Operators
* Logical Operators
* Membership Operators
* Identity Operators
* Expressions
* Operator Precedence

Get ready to make decisions and comparisons in Python!
