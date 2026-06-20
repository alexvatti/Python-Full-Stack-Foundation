# Python Full Stack Foundation

# Week 3 – Day 11

## for Loop, range(), Loop Patterns

---

# Learning Objectives

By the end of this session, learners will be able to:

* Understand Repetition in Programming
* Understand Iteration
* Learn Lists, Tuples, Sets, Dictionaries, and Strings (High-Level)
* Use `for` Loops
* Use `range()`
* Create Number Patterns
* Iterate Through Collections
* Build Real-World Programs

---

# Recap

Previously we learned:

* if Statement
* if-else Statement
* if-elif-else Statement
* Nested if
* Multiple Conditions

Until now, statements executed once.

Today we learn how to execute statements multiple times.

---

# 1. Why Do We Need Loops?

Suppose we want to print:

```text
Python
Python
Python
Python
Python
```

Without loops:

```python
print("Python")
print("Python")
print("Python")
print("Python")
print("Python")
```

Not efficient.

Using loops:

```python
for i in range(5):
    print("Python")
```

Output

```text
Python
Python
Python
Python
Python
```

---

# What is a Loop?

A loop repeats a block of code.

```text
Repeat
Repeat
Repeat
Repeat
Until Condition Ends
```

---

# Types of Loops in Python

| Loop  | Purpose             |
| ----- | ------------------- |
| for   | Known Repetitions   |
| while | Unknown Repetitions |

Today:

```text
for Loop
```

---

# Before Learning for Loop

# Collections Overview

A collection stores multiple values.

Python provides:

* List
* Tuple
* Set
* Dictionary
* String

We will learn them in detail later.

Today only a high-level introduction.

---

# List

Stores multiple values.

```python
subjects = ["Python", "SQL", "HTML"]
```

Visual

```text
Python
SQL
HTML
```

---

# Tuple

Similar to list but immutable.

```python
subjects = ("Python", "SQL", "HTML")
```

---

# Set

Stores unique values.

```python
subjects = {"Python", "SQL", "HTML"}
```

Duplicate values are removed.

---

# Dictionary

Stores key-value pairs.

```python
student = {
    "name":"Alex",
    "city":"Hyderabad"
}
```

---

# String

Collection of characters.

```python
name = "Python"
```

Visual

```text
P Y T H O N
```

---

# Common Idea

All these collections contain multiple values.

We can use loops to access them.

---

# 2. What is a for Loop?

A for loop is used to iterate over a collection.

---

# Syntax

```python
for variable in collection:
    statements
```

---

# Flow

```text
Collection
     ↓
First Item
     ↓
Execute

Second Item
     ↓
Execute

Third Item
     ↓
Execute

Continue Until End
```

---

# Example 1

```python
for i in [1,2,3,4,5]:
    print(i)
```

Output

```text
1
2
3
4
5
```

---

# Understanding

Iteration 1

```text
i = 1
```

Iteration 2

```text
i = 2
```

Iteration 3

```text
i = 3
```

and so on.

---

# Example 2

```python
for item in ["Python","SQL","HTML"]:
    print(item)
```

Output

```text
Python
SQL
HTML
```

---

# Example 3

```python
for x in (10,20,30):
    print(x)
```

Output

```text
10
20
30
```

---

# Example 4

```python
for x in {"Python","SQL","HTML"}:
    print(x)
```

Output

```text
Python
SQL
HTML
```

Order may vary in sets.

---

# Example 5

```python
name = "Python"

for ch in name:
    print(ch)
```

Output

```text
P
y
t
h
o
n
```

---

# Example 6

Dictionary Loop

```python
student = {
    "name":"Alex",
    "city":"Hyderabad"
}

for key in student:
    print(key)
```

Output

```text
name
city
```

---

# Dictionary Keys and Values

```python
student = {
    "name":"Alex",
    "city":"Hyderabad"
}

for key in student:
    print(key, student[key])
```

Output

```text
name Alex
city Hyderabad
```

---

# 3. range() Function

Very important with for loops.

---

# What is range()?

Generates a sequence of numbers.

---

# Syntax 1

```python
range(stop)
```

---

# Example

```python
for i in range(5):
    print(i)
```

Output

```text
0
1
2
3
4
```

---

# Why Not 5?

Because:

```text
Start = 0
Stop = 5
Stop Value Excluded
```

---

# Syntax 2

```python
range(start, stop)
```

---

# Example

```python
for i in range(1,6):
    print(i)
```

Output

```text
1
2
3
4
5
```

---

# Syntax 3

```python
range(start, stop, step)
```

---

# Example

```python
for i in range(1,11,2):
    print(i)
```

Output

```text
1
3
5
7
9
```

---

# Even Numbers

```python
for i in range(2,11,2):
    print(i)
```

Output

```text
2
4
6
8
10
```

---

# Reverse Counting

```python
for i in range(10,0,-1):
    print(i)
```

Output

```text
10
9
8
7
6
5
4
3
2
1
```

---

# 4. Real World Examples

# Print Student Roll Numbers

```python
for roll in range(1,11):
    print(roll)
```

---

# Print Employee IDs

```python
for emp in range(1001,1006):
    print(emp)
```

---

# Print Multiplication Table of 5

```python
for i in range(1,11):
    print(5 * i)
```

Output

```text
5
10
15
20
25
30
35
40
45
50
```

---

# Better Format

```python
for i in range(1,11):
    print(f"5 x {i} = {5*i}")
```

---

# Sum of Numbers

```python
total = 0

for i in range(1,6):
    total += i

print(total)
```

Output

```text
15
```

---

# 5. Loop Patterns

Patterns are common interview and practice questions.

---

# Pattern 1

```python
for i in range(5):
    print("*")
```

Output

```text
*
*
*
*
*
```

---

# Pattern 2

```python
for i in range(5):
    print("*****")
```

Output

```text
*****
*****
*****
*****
*****
```

---

# Pattern 3

```python
for i in range(1,6):
    print(i)
```

Output

```text
1
2
3
4
5
```

---

# Pattern 4

```python
for i in range(1,6):
    print(i * "*")
```

Output

```text
*
**
***
****
*****
```

---

# Pattern 5

```python
for i in range(5,0,-1):
    print(i * "*")
```

Output

```text
*****
****
***
**
*
```

---

# Nested Loop Preview

```python
for row in range(3):

    for col in range(3):
        print("*", end=" ")

    print()
```

Output

```text
* * *
* * *
* * *
```

We will learn nested loops later.

---

# Mini Project 1

Print Numbers 1 to 10

```python
for i in range(1,11):
    print(i)
```

---

# Mini Project 2

Print Even Numbers

```python
for i in range(2,21,2):
    print(i)
```

---

# Mini Project 3

Print Odd Numbers

```python
for i in range(1,21,2):
    print(i)
```

---

# Mini Project 4

Multiplication Table

```python
num = 7

for i in range(1,11):
    print(f"{num} x {i} = {num*i}")
```

---

# Mini Project 5

Display Subjects

```python
subjects = ["Python","SQL","HTML"]

for subject in subjects:
    print(subject)
```

---

# Practice Exercises

## Exercise 1

Print 1 to 20.

---

## Exercise 2

Print 20 to 1.

---

## Exercise 3

Print Even Numbers.

---

## Exercise 4

Print Odd Numbers.

---

## Exercise 5

Print Multiples of 5.

---

## Exercise 6

Print Student Names from List.

---

## Exercise 7

Print Characters of String.

---

## Exercise 8

Print Dictionary Keys and Values.

---

## Exercise 9

Print Table of 12.

---

## Exercise 10

Print Pattern

```text
*
**
***
****
*****
```

---

# Quick Summary

| Topic      | Description               |
| ---------- | ------------------------- |
| Loop       | Repeats Code              |
| for        | Iteration Loop            |
| range()    | Generates Numbers         |
| List       | Ordered Collection        |
| Tuple      | Immutable Collection      |
| Set        | Unique Values             |
| Dictionary | Key-Value Pairs           |
| String     | Collection of Characters  |
| Pattern    | Repeated Output Structure |

---

# Session Summary

Today we learned:

✔ Introduction to Collections

✔ List

✔ Tuple

✔ Set

✔ Dictionary

✔ String

✔ for Loop

✔ range()

✔ Iteration

✔ Multiplication Tables

✔ Patterns

✔ Real-World Examples

---

# Homework

1. Print Numbers 1 to 100.
2. Print Even Numbers from 1 to 50.
3. Print Odd Numbers from 1 to 50.
4. Print Multiplication Tables from 1 to 10.
5. Loop Through a List of Subjects.
6. Loop Through a String.
7. Loop Through a Dictionary.
8. Create 5 Star Patterns.
9. Find Sum of Numbers 1 to 100.
10. Find Sum of Even Numbers from 1 to 50.

---

