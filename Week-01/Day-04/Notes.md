# Python Full Stack Foundation

# Week 1 – Day 4

## Relational Operators, Logical Operators, Membership Operators, Identity Operators

---

# Learning Objectives

By the end of this session, learners will be able to:

* Compare values using Relational Operators
* Combine conditions using Logical Operators
* Check membership using Membership Operators
* Compare object identity using Identity Operators
* Understand Boolean values
* Build decision-making logic
* Solve real-world comparison problems

---

# Recap of Day 3

Previously we learned:

* Type Casting
* Arithmetic Operators
* Assignment Operators
* Calculator Programs

Today we will learn how to compare values and create conditions.

---

# 1. Introduction to Boolean Values

Many programming decisions are based on two values:

```text
True
False
```

Examples:

* Is age greater than 18?
* Is salary greater than 50000?
* Is student present?
* Is password correct?

The answer is always:

```text
True
or
False
```

---

# What Produces True or False?

Operators such as:

* Relational Operators
* Logical Operators
* Membership Operators
* Identity Operators

---

# 2. Relational Operators

Relational Operators compare values.

---

# Relational Operator Table

| Operator | Meaning                  |
| -------- | ------------------------ |
| ==       | Equal To                 |
| !=       | Not Equal To             |
| >        | Greater Than             |
| <        | Less Than                |
| >=       | Greater Than or Equal To |
| <=       | Less Than or Equal To    |

---

# Equal To (==)

Checks whether two values are equal.

```python
print(10 == 10)
```

Output

```text
True
```

---

```python
print(10 == 20)
```

Output

```text
False
```

---

# Not Equal To (!=)

```python
print(10 != 20)
```

Output

```text
True
```

---

```python
print(10 != 10)
```

Output

```text
False
```

---

# Greater Than (>)

```python
print(20 > 10)
```

Output

```text
True
```

---

```python
print(10 > 20)
```

Output

```text
False
```

---

# Less Than (<)

```python
print(10 < 20)
```

Output

```text
True
```

---

```python
print(20 < 10)
```

Output

```text
False
```

---

# Greater Than or Equal To (>=)

```python
print(20 >= 20)
```

Output

```text
True
```

---

```python
print(10 >= 20)
```

Output

```text
False
```

---

# Less Than or Equal To (<=)

```python
print(10 <= 20)
```

Output

```text
True
```

---

```python
print(20 <= 10)
```

Output

```text
False
```

---

# Real World Example

```python
age = 21

print(age >= 18)
```

Output

```text
True
```

Interpretation:

```text
Eligible for Voting
```

---

# Marks Example

```python
marks = 75

print(marks >= 35)
```

Output

```text
True
```

Interpretation:

```text
Student Passed
```

---

# 3. Logical Operators

Logical Operators combine multiple conditions.

---

# Logical Operator Table

| Operator | Meaning                             |
| -------- | ----------------------------------- |
| and      | Both Conditions Must Be True        |
| or       | At Least One Condition Must Be True |
| not      | Reverses Result                     |

---

# AND Operator

Returns True only if both conditions are True.

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

# AND Truth Table

| Condition 1 | Condition 2 | Result |
| ----------- | ----------- | ------ |
| True        | True        | True   |
| True        | False       | False  |
| False       | True        | False  |
| False       | False       | False  |

---

# Example

```python
age = 25
salary = 60000

print(age > 18 and salary > 50000)
```

Output

```text
True
```

---

# OR Operator

Returns True if at least one condition is True.

```python
print(True or False)
```

Output

```text
True
```

---

```python
print(False or False)
```

Output

```text
False
```

---

# OR Truth Table

| Condition 1 | Condition 2 | Result |
| ----------- | ----------- | ------ |
| True        | True        | True   |
| True        | False       | True   |
| False       | True        | True   |
| False       | False       | False  |

---

# Example

```python
attendance = 80
sports_quota = True

print(attendance >= 75 or sports_quota)
```

Output

```text
True
```

---

# NOT Operator

Reverses the result.

```python
print(not True)
```

Output

```text
False
```

---

```python
print(not False)
```

Output

```text
True
```

---

# Example

```python
is_logged_in = True

print(not is_logged_in)
```

Output

```text
False
```

---

# 4. Membership Operators

Membership Operators check whether a value exists in a collection.

---

# Membership Operator Table

| Operator | Meaning        |
| -------- | -------------- |
| in       | Exists         |
| not in   | Does Not Exist |

---

# Using in

```python
name = "Python"

print("P" in name)
```

Output

```text
True
```

---

```python
print("Z" in name)
```

Output

```text
False
```

---

# List Example

```python
subjects = ["Python", "SQL", "HTML"]

print("Python" in subjects)
```

Output

```text
True
```

---

```python
print("Java" in subjects)
```

Output

```text
False
```

---

# Using not in

```python
subjects = ["Python", "SQL", "HTML"]

print("Java" not in subjects)
```

Output

```text
True
```

---

```python
print("Python" not in subjects)
```

Output

```text
False
```

---

# Real World Example

```python
allowed_users = ["Alex", "John", "Mary"]

print("Alex" in allowed_users)
```

Output

```text
True
```

Meaning:

```text
User Exists
```

---

# 5. Identity Operators

Identity Operators compare memory locations.

---

# Identity Operator Table

| Operator | Meaning          |
| -------- | ---------------- |
| is       | Same Object      |
| is not   | Different Object |

---

# Example

```python
x = 100
y = 100

print(x is y)
```

Output

```text
True
```

---

# Another Example

```python
a = [1,2,3]
b = [1,2,3]

print(a == b)
```

Output

```text
True
```

Values are equal.

---

```python
print(a is b)
```

Output

```text
False
```

Different memory locations.

---

# Understanding == vs is

## ==

Compares Values

```python
a = [1,2,3]
b = [1,2,3]

print(a == b)
```

Output

```text
True
```

---

## is

Compares Memory Locations

```python
a = [1,2,3]
b = [1,2,3]

print(a is b)
```

Output

```text
False
```

---

# Example Using is not

```python
a = [1,2,3]
b = [1,2,3]

print(a is not b)
```

Output

```text
True
```

---

# Combined Examples

```python
age = 25

print(age >= 18 and age <= 60)
```

Output

```text
True
```

---

```python
name = "Python"

print("P" in name and len(name) > 3)
```

Output

```text
True
```

---

# Mini Project 1

Voting Eligibility Checker

```python
age = int(input("Enter Age: "))

print(age >= 18)
```

Output

```text
True
```

---

# Mini Project 2

Login Checker

```python
username = input("Enter Username: ")

users = ["Alex", "John", "Mary"]

print(username in users)
```

---

# Mini Project 3

College Eligibility

```python
marks = int(input("Enter Marks: "))
sports = True

print(marks >= 75 or sports)
```

---

# Practice Exercises

## Exercise 1

Check:

```python
20 > 10
```

---

## Exercise 2

Check:

```python
50 == 50
```

---

## Exercise 3

Check:

```python
100 != 50
```

---

## Exercise 4

Use AND operator with age and salary.

---

## Exercise 5

Use OR operator with attendance and sports quota.

---

## Exercise 6

Check if "Python" exists in a list.

---

## Exercise 7

Check if "Java" is not present in a list.

---

## Exercise 8

Create two lists and compare using:

```python
==
is
is not
```

---

# Quick Summary

| Topic  | Description              |
| ------ | ------------------------ |
| ==     | Equal To                 |
| !=     | Not Equal To             |
| >      | Greater Than             |
| <      | Less Than                |
| >=     | Greater Than or Equal To |
| <=     | Less Than or Equal To    |
| and    | Both True                |
| or     | Any One True             |
| not    | Reverse Result           |
| in     | Membership Check         |
| not in | Membership Absence Check |
| is     | Same Object              |
| is not | Different Object         |

---

# Session Summary

Today we learned:

✔ Boolean Values

✔ Relational Operators

✔ Logical Operators

✔ Membership Operators

✔ Identity Operators

✔ == vs is

✔ Truth Tables

✔ Real World Comparisons

✔ Eligibility Checking

✔ User Validation

---

# Homework

1. Check Voting Eligibility.
2. Check Student Pass/Fail Eligibility.
3. Create a Login Validation Program.
4. Practice all Relational Operators.
5. Practice all Logical Operators.
6. Practice Membership Operators using Lists.
7. Compare == and is using Lists.
8. Create 10 examples for each operator category.

---

# Next Session Preview

## Week 1 – Day 5

* Expressions
* Operator Precedence
* Mini Practice Problems
* Calculator Project

Get ready to combine everything learned in Week 1 and build practical Python programs!
