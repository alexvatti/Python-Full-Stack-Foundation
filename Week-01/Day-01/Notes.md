# Python Full Stack Foundation

# Week 1 – Day 1

## Introduction to Programming, Problem Solving, Python Installation, VS Code Setup, First Program, print()

---

# Learning Objectives

By the end of this session, learners will be able to:

* Understand what programming is
* Understand why programming is useful
* Learn the basic problem-solving approach
* Install Python
* Install VS Code
* Run a Python program
* Write the first Python program
* Use the `print()` function
* Understand basic string formatting techniques

---

# 1. What is Programming?

Programming is the process of giving instructions to a computer to perform a task.

Just like humans follow instructions, computers also follow instructions. These instructions are written using a programming language.

## Example 1 – Human Instructions

1. Wake up
2. Brush teeth
3. Have breakfast
4. Go to office

## Example 2 – Computer Instructions

1. Read user input
2. Add two numbers
3. Display result

These instructions written for a computer are called a **program**.

---

# 2. Why Learn Programming?

Programming helps us:

* Automate repetitive tasks
* Build websites
* Create mobile applications
* Analyze data
* Build Artificial Intelligence systems
* Create games
* Solve business problems

## Real World Examples

| Application | Usage           |
| ----------- | --------------- |
| ATM         | Withdraw money  |
| WhatsApp    | Messaging       |
| Google Maps | Navigation      |
| Amazon      | Online Shopping |
| YouTube     | Video Streaming |

All these applications are built using programming.

---

# 3. What is a Programming Language?

A programming language is a language used to communicate with computers.

## Popular Programming Languages

| Language   | Usage                           |
| ---------- | ------------------------------- |
| Python     | AI, ML, Web Development         |
| Java       | Enterprise Applications         |
| JavaScript | Web Applications                |
| C          | System Programming              |
| C++        | Games, High Performance Systems |

---

# 4. Why Python?

Python is one of the most popular programming languages.

## Advantages of Python

* Easy to Learn
* Easy to Read
* Simple Syntax
* Large Community Support
* Cross Platform
* Used in AI and Machine Learning
* Used in Data Science
* Used in Web Development

## Companies Using Python

* Google
* Netflix
* Instagram
* Spotify
* Dropbox
* NASA

---

# 5. Problem Solving Approach

Every programmer follows a structured approach.

---

## Step 1: Understand the Problem

### Example

Add two numbers and display the result.

---

## Step 2: Identify Inputs

### Input

* Number 1
* Number 2

Example:

```text
10
20
```

---

## Step 3: Identify the Process

```text
Result = Number1 + Number2
```

---

## Step 4: Identify Output

```text
30
```

---

# Generic Problem Solving Template

## Problem

Find the sum of two numbers.

### Input

* Number A
* Number B

### Process

```text
A + B
```

### Output

```text
Sum
```

---

# Activity 1

## Problem

Find the area of a rectangle.

### Input

* Length
* Width

### Process

```text
Length × Width
```

### Output

```text
Area
```

---

# Activity 2

## Problem

Calculate Simple Interest.

### Input

* Principal
* Rate
* Time

### Process

```text
(P × R × T) / 100
```

### Output

```text
Simple Interest
```

---

# 6. Installing Python

## Step 1

Visit:

```text
https://www.python.org
```

---

## Step 2

Click Downloads.

---

## Step 3

Download the latest stable version.

Example:

```text
Python 3.x
```

---

## Step 4

Run the installer.

### Important

✔ Check:

```text
Add Python to PATH
```

---

## Step 5

Click:

```text
Install Now
```

---

## Verify Installation

Open Command Prompt or Terminal.

```bash
python --version
```

Expected Output:

```bash
Python 3.x.x
```

---

# 7. Installing VS Code

## Step 1

Visit:

```text
https://code.visualstudio.com
```

---

## Step 2

Download VS Code.

---

## Step 3

Install using default settings.

---

## Step 4

Open VS Code.

---

## Step 5

Install Python Extension.

Search:

```text
Python
```

Publisher:

```text
Microsoft
```

Click Install.

---

# Creating First Python File

## Step 1

Open VS Code.

---

## Step 2

Create Folder

```text
PythonTraining
```

---

## Step 3

Create File

```text
day1.py
```

---

## Step 4

Write Code

```python
print("Hello World")
```

---

## Step 5

Run Program

Method 1:

```text
Run ▶
```

Method 2:

```bash
python day1.py
```

---

# 8. First Python Program

```python
print("Hello World")
```

Output:

```text
Hello World
```

---

# Understanding the Program

```python
print("Hello World")
```

### print

Built-in Python function.

### "Hello World"

Text to display.

### Output

Displays text on the screen.

---

# More Examples

## Example 1

```python
print("Welcome to Python")
```

Output

```text
Welcome to Python
```

---

## Example 2

```python
print("My Name is Alex")
```

Output

```text
My Name is Alex
```

---

## Example 3

```python
print(100)
```

Output

```text
100
```

---

# 9. The print() Function

The `print()` function displays information on the screen.

## Syntax

```python
print(value)
```

---

## 9.1 Printing Text

```python
print("Python")
```

Output

```text
Python
```

---

## 9.2 Printing Numbers

```python
print(100)
```

Output

```text
100
```

---

## 9.3 Printing Decimal Numbers

```python
print(99.99)
```

Output

```text
99.99
```

---

## 9.4 Printing Boolean Values

```python
print(True)
print(False)
```

Output

```text
True
False
```

---

## 9.5 Printing Multiple Values

```python
print("Age", 25)
```

Output

```text
Age 25
```

---

## 9.6 Printing Multiple Lines

```python
print("Python")
print("Java")
print("SQL")
```

Output

```text
Python
Java
SQL
```

---

## 9.7 New Line Character

```python
print("Python\nJava\nSQL")
```

Output

```text
Python
Java
SQL
```

---

## 9.8 Separator (sep)

Default Separator:

```python
print("Python", "Java", "SQL")
```

Output

```text
Python Java SQL
```

Custom Separator:

```python
print("Python", "Java", "SQL", sep="-")
```

Output

```text
Python-Java-SQL
```

---

## 9.9 End Parameter

Default:

```python
print("Hello")
print("World")
```

Output

```text
Hello
World
```

Custom:

```python
print("Hello", end=" ")
print("World")
```

Output

```text
Hello World
```

---

## 9.10 Escape Characters

```python
print("I am learning \"Python\"")
```

Output

```text
I am learning "Python"
```

---

# 10. String Formatting

String Formatting helps combine text and values.

---

## Method 1: String Concatenation

```python
name = "Alex"

print("Hello " + name)
```

Output

```text
Hello Alex
```

---

### Multiple Strings

```python
first_name = "Alex"
last_name = "Kumar"

print(first_name + " " + last_name)
```

Output

```text
Alex Kumar
```

---

### Concatenating String and Number

```python
name = "Alex"
age = 25

print("Name: " + name)
print("Age: " + str(age))
```

Output

```text
Name: Alex
Age: 25
```

---

## Method 2: format()

```python
name = "Alex"
age = 25

print("Name: {}".format(name))
print("Age: {}".format(age))
```

Output

```text
Name: Alex
Age: 25
```

---

### Multiple Placeholders

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

### Named Placeholders

```python
print("Name: {n} Age: {a}".format(n="Alex", a=25))
```

Output

```text
Name: Alex Age: 25
```

---

## Method 3: f-Strings

Recommended in modern Python.

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

### Multiple Variables

```python
name = "Alex"
age = 25

print(f"Name: {name}, Age: {age}")
```

Output

```text
Name: Alex, Age: 25
```

---

### Expressions Inside f-Strings

```python
a = 10
b = 20

print(f"Sum = {a+b}")
```

Output

```text
Sum = 30
```

---

### Decimal Formatting

```python
pi = 3.14159265

print(f"{pi:.2f}")
```

Output

```text
3.14
```

---

# Comparison of Formatting Methods

```python
name = "Alex"
salary = 50000
```

### Concatenation

```python
print("Name: " + name + " Salary: " + str(salary))
```

### format()

```python
print("Name: {} Salary: {}".format(name, salary))
```

### f-String

```python
print(f"Name: {name} Salary: {salary}")
```

Output

```text
Name: Alex Salary: 50000
```

---

# Quick Summary

| Method          | Example                   |
| --------------- | ------------------------- |
| Basic Print     | `print("Python")`         |
| Multiple Values | `print("Age",25)`         |
| Separator       | `print("A","B",sep="-")`  |
| End             | `print("Hello",end=" ")`  |
| Concatenation   | `"Hello " + name`         |
| format()        | `"Hello {}".format(name)` |
| f-String        | `f"Hello {name}"`         |

### Recommended

✅ Use **f-Strings** in modern Python programs.

---

# Practice Exercises

## Exercise 1

Display your name.

```python
print("Alex")
```

---

## Exercise 2

Display your city.

```python
print("Hyderabad")
```

---

## Exercise 3

Display your favorite subject.

```python
print("Python")
```

---

## Exercise 4

Display three lines using three print statements.

---

## Exercise 5

Display:

```text
Welcome
To
Python
Programming
```

---

## Exercise 6

Display your name and age using:

* Concatenation
* format()
* f-String

---

# Mini Assignment

Write a Python program to display:

```text
Student Name : __________
Course       : Python Full Stack Foundation
Day          : Day 1
```

Use all three methods:

* Concatenation
* format()
* f-String

---

# Session Summary

Today we learned:

✔ What is Programming

✔ Why Programming is Important

✔ Programming Languages

✔ Why Python

✔ Problem Solving Approach

✔ Python Installation

✔ VS Code Installation

✔ First Python Program

✔ print() Function

✔ sep Parameter

✔ end Parameter

✔ Escape Characters

✔ String Concatenation

✔ format()

✔ f-Strings

✔ Practice Programs

---

# Homework

1. Install Python.
2. Install VS Code.
3. Create a folder named `PythonPractice`.
4. Create 5 programs using `print()`.
5. Display:

   * Name
   * City
   * College
   * Favorite Subject
   * Career Goal
6. Create one program using Concatenation.
7. Create one program using format().
8. Create one program using f-String.

---

# Next Session Preview

## Week 1 – Day 2

* Variables
* Data Types
* Naming Rules
* Comments
* Input Function
* Output Function

Get ready to write interactive Python programs!
