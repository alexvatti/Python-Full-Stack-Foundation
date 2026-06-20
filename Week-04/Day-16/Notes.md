# Python Full Stack Foundation

# Week-04 – Day-16

# Python Built-in Modules

## math Module & os Module

---

# Learning Objectives

By the end of this session, learners will be able to:

- Understand Python Modules
- Import Modules
- Use the math Module
- Use the os Module
- Perform Mathematical Operations
- Work with Files and Directories
- Get Current Working Directory
- Create and Remove Folders
- Rename Files and Folders
- Execute Common OS Operations

---
## `help()` and `dir()`

Python provides two useful built-in functions for exploring modules, functions, and objects.

### `help()`
Displays the documentation of a module, function, class, or object.

```python
import math
help(math)
help(math.sqrt)
```

### `dir()`
Returns a list of all available attributes, methods, and functions.

```python
import math
print(dir(math))

numbers = [10, 20, 30]
print(dir(numbers))
```

# 1. What is a Module?

## Definition

A **Module** is a Python file that contains functions, classes, and variables that can be reused in multiple programs.

Python provides:

- Built-in Modules
- User-defined Modules
- Third-party Modules

Examples:

- math
- os
- random
- datetime
- statistics

---

# Why Modules?

Without Modules

```
Write everything yourself
```

With Modules

```
Import
Reuse
Save Time
```

---

# Importing Modules

## Import Entire Module

```python
import math

print(math.sqrt(25))
```

---

## Import Specific Function

```python
from math import sqrt

print(sqrt(25))
```

---

## Import with Alias

```python
import math as m

print(m.pi)
```

---

# 2. math Module

The **math** module provides mathematical functions and constants.

```python
import math
```

---

# Constants

## pi

```python
import math

print(math.pi)
```

Output

```
3.141592653589793
```

---

## e

```python
print(math.e)
```

Output

```
2.718281828459045
```

---

# Square Root

```python
import math

print(math.sqrt(64))
```

Output

```
8.0
```

---

# Power

```python
import math

print(math.pow(2,5))
```

Output

```
32.0
```

---

# Absolute Value

```python
print(abs(-25))
```

Output

```
25
```

---

# Ceiling

Rounds upward.

```python
import math

print(math.ceil(4.2))
```

Output

```
5
```

---

# Floor

Rounds downward.

```python
import math

print(math.floor(4.8))
```

Output

```
4
```

---

# Factorial

```python
import math

print(math.factorial(5))
```

Output

```
120
```

---

# GCD

```python
import math

print(math.gcd(12,18))
```

Output

```
6
```

---

# Trigonometric Functions

```python
import math

print(math.sin(math.radians(90)))
print(math.cos(math.radians(0)))
print(math.tan(math.radians(45)))
```

Output

```
1.0
1.0
0.9999999999999999
```

---

# Logarithm

```python
import math

print(math.log10(100))
```

Output

```
2.0
```

---

# Exponential

```python
import math

print(math.exp(2))
```

Output

```
7.38905609893065
```

---

# Common math Functions

| Function | Purpose |
|----------|---------|
| sqrt() | Square Root |
| pow() | Power |
| ceil() | Round Up |
| floor() | Round Down |
| factorial() | Factorial |
| gcd() | Greatest Common Divisor |
| sin() | Sine |
| cos() | Cosine |
| tan() | Tangent |
| log() | Logarithm |
| exp() | Exponential |

---

# Practical Example

Area of Circle

```python
import math

radius = 7

area = math.pi * radius ** 2

print(area)
```

---

# 3. os Module

The **os** module allows Python to interact with the operating system.

```python
import os
```

---

# Current Working Directory

```python
import os

print(os.getcwd())
```

---

# Change Directory

```python
import os

os.chdir("D:/Python")

print(os.getcwd())
```

---

# List Files

```python
import os

print(os.listdir())
```

---

# Create Folder

```python
import os

os.mkdir("Projects")
```

---

# Create Nested Folder

```python
import os

os.makedirs("Python/Week4")
```

---

# Rename Folder/File

```python
import os

os.rename("Projects","PythonProjects")
```

---

# Remove Empty Folder

```python
import os

os.rmdir("PythonProjects")
```

---

# Remove Nested Folder

```python
import os

os.removedirs("Python/Week4")
```

---

# Delete File

```python
import os

os.remove("sample.txt")
```

---

# Check File Exists

```python
import os

print(os.path.exists("sample.txt"))
```

Output

```
True
```

---

# Check File

```python
print(os.path.isfile("sample.txt"))
```

---

# Check Folder

```python
print(os.path.isdir("Python"))
```

---

# Join Paths

```python
import os

path = os.path.join("Users","Alex","Documents")

print(path)
```

---

# Get Environment Variables

```python
import os

print(os.environ)
```

---

# Get Operating System Name

```python
import os

print(os.name)
```

Output (Windows)

```
nt
```

Output (Linux/Mac)

```
posix
```

---

# Execute Operating System Command

Windows

```python
import os

os.system("dir")
```

Linux / Mac

```python
import os

os.system("ls")
```

---

# Common os Module Functions

| Function | Purpose |
|----------|---------|
| getcwd() | Current Directory |
| chdir() | Change Directory |
| listdir() | List Files |
| mkdir() | Create Folder |
| makedirs() | Create Nested Folders |
| rename() | Rename |
| remove() | Delete File |
| rmdir() | Remove Folder |
| removedirs() | Remove Nested Folders |
| path.exists() | Check Existence |
| path.isfile() | Check File |
| path.isdir() | Check Folder |
| path.join() | Join Paths |
| system() | Execute Command |

---

# Practical Programs

## Program 1

Find Square Root

```python
import math

num = int(input("Enter Number: "))

print(math.sqrt(num))
```

---

## Program 2

Area of Circle

```python
import math

r = float(input("Radius: "))

print(math.pi * r * r)
```

---

## Program 3

Display All Files

```python
import os

for file in os.listdir():
    print(file)
```

---

## Program 4

Create Folder

```python
import os

folder = input("Folder Name: ")

os.mkdir(folder)

print("Folder Created")
```

---

## Program 5

Check File Exists

```python
import os

file = input("Enter File Name: ")

if os.path.exists(file):
    print("File Exists")
else:
    print("File Not Found")
```

---

# Quick Summary

| Module | Purpose |
|---------|---------|
| math | Mathematical Calculations |
| os | Operating System Operations |
| sqrt() | Square Root |
| ceil() | Round Up |
| floor() | Round Down |
| factorial() | Factorial |
| gcd() | Greatest Common Divisor |
| getcwd() | Current Folder |
| listdir() | List Files |
| mkdir() | Create Folder |
| rename() | Rename |
| remove() | Delete File |

---

# Homework

1. Find the square root of a number.
2. Calculate the area of a circle.
3. Find the factorial of a number.
4. Display all files in the current directory.
5. Create a new folder.
6. Rename the folder.
7. Delete the folder.
8. Check whether a file exists.
9. Print the current working directory.
10. Display the operating system name.

---

# Session Summary

Today we learned:

✔ Python Modules

✔ Import Statements

✔ math Module

✔ os Module

✔ Mathematical Functions

✔ Directory Operations

✔ File Operations

✔ Path Operations

✔ Real-World Examples

---

# Next Session Preview

## Week-04 – Day-17

- random Module
- datetime Module
- time Module
- calendar Module
- Python Package Management
- Creating User-Defined Modules
