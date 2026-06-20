# Python Full Stack Foundation

# Week-03 – Day-14

# File Handling in Python

---

# Learning Objectives

By the end of this session, learners will be able to:

- Understand File Handling
- Open Files
- Read File Contents
- Write to Files
- Append Data to Files
- Close Files
- Use the `with` Statement
- Rename Files
- Delete Files
- Check if a File Exists
- Perform Common File Operations
- Handle File Exceptions

---

# Recap

Previously we learned:

- Functions
- Exception Handling

Today we will learn how Python works with files.

---

# 1. What is File Handling?

## Definition

**File Handling** is the process of creating, opening, reading, writing, appending, renaming, and deleting files using Python.

Files allow data to be stored permanently, even after the program ends.

---

## Why File Handling?

Without Files

```
Program Ends
      ↓
Data Lost
```

With Files

```
Program Ends
      ↓
Data Saved
      ↓
Available Next Time
```

---

## Real-World Examples

- Student Records
- Employee Details
- Bank Transactions
- Login Credentials
- Reports
- Log Files
- Configuration Files

---

# 2. Types of Files

Python mainly works with two types of files.

| File Type | Description | Example |
|------------|-------------|---------|
| Text File | Human-readable | .txt, .csv |
| Binary File | Stores binary data | .jpg, .pdf, .mp3 |

In this session, we focus on **Text Files**.

---

# 3. Opening a File

Use the built-in `open()` function.

## Syntax

```python
file = open(filename, mode)
```

---

## Example

```python
file = open("sample.txt", "r")
```

---

# 4. File Modes

| Mode | Description |
|------|-------------|
| r | Read |
| w | Write |
| a | Append |
| x | Create New File |
| r+ | Read and Write |
| w+ | Write and Read |
| a+ | Append and Read |
| rb | Read Binary |
| wb | Write Binary |
| ab | Append Binary |

---

# 5. Reading a File

Suppose **sample.txt** contains:

```
Python
SQL
HTML
```

---

## read()

Reads the entire file.

```python
file = open("sample.txt", "r")

data = file.read()

print(data)

file.close()
```

Output

```
Python
SQL
HTML
```

---

## readline()

Reads one line at a time.

```python
file = open("sample.txt", "r")

print(file.readline())
print(file.readline())

file.close()
```

Output

```
Python

SQL
```

---

## readlines()

Returns all lines as a list.

```python
file = open("sample.txt", "r")

lines = file.readlines()

print(lines)

file.close()
```

Output

```
['Python\n', 'SQL\n', 'HTML']
```

---

## Reading Using Loop

```python
file = open("sample.txt", "r")

for line in file:
    print(line.strip())

file.close()
```

Output

```
Python
SQL
HTML
```

---

# 6. Writing to a File

Mode: **w**

Creates a new file if it doesn't exist.

If the file already exists, all previous content is erased.

```python
file = open("sample.txt", "w")

file.write("Python\n")
file.write("SQL\n")

file.close()
```

File Content

```
Python
SQL
```

---

# 7. Appending to a File

Mode: **a**

Adds new data to the end of the file.

```python
file = open("sample.txt", "a")

file.write("HTML\n")

file.close()
```

File Content

```
Python
SQL
HTML
```

---

# Difference Between w and a

| Write (w) | Append (a) |
|------------|------------|
| Deletes existing content | Keeps existing content |
| Starts from beginning | Adds at the end |

---

# 8. Creating a New File

Mode: **x**

```python
file = open("student.txt", "x")

file.close()
```

If the file already exists,

Output

```
FileExistsError
```

---

# 9. Closing a File

Always close files after use.

```python
file = open("sample.txt", "r")

print(file.read())

file.close()
```

---

# Why Close Files?

- Saves data properly
- Releases system resources
- Prevents memory leaks

---

# 10. Using with Statement

Recommended method.

Automatically closes the file.

```python
with open("sample.txt", "r") as file:

    print(file.read())
```

No need to call `close()`.

---

# 11. File Pointer

The file pointer indicates the current reading position.

```python
file = open("sample.txt", "r")

print(file.read(6))

print(file.read())

file.close()
```

Output

```
Python
SQL
HTML
```

The second `read()` continues from where the first one stopped.

---

# 12. tell()

Returns the current file pointer position.

```python
file = open("sample.txt", "r")

print(file.tell())

file.read(5)

print(file.tell())

file.close()
```

Example Output

```
0
5
```

---

# 13. seek()

Moves the file pointer.

```python
file = open("sample.txt", "r")

file.seek(0)

print(file.read())

file.close()
```

---

# 14. Renaming a File

Use the `os` module.

```python
import os

os.rename("sample.txt", "python.txt")
```

---

# 15. Deleting a File

```python
import os

os.remove("python.txt")
```

---

# 16. Check Whether File Exists

```python
import os

if os.path.exists("sample.txt"):
    print("File Exists")
else:
    print("File Not Found")
```

---

# 17. Handling File Exceptions

```python
try:

    file = open("sample.txt", "r")

    print(file.read())

except FileNotFoundError:

    print("File Not Found")
```

---

# Using finally

```python
try:

    file = open("sample.txt", "r")

    print(file.read())

except FileNotFoundError:

    print("File Not Found")

finally:

    print("Program Finished")
```

---

# 18. Practical Example 1

Write Student Names

```python
with open("students.txt", "w") as file:

    file.write("Alex\n")
    file.write("John\n")
    file.write("Mary\n")
```

---

# Practical Example 2

Read Student Names

```python
with open("students.txt", "r") as file:

    for student in file:
        print(student.strip())
```

---

# Practical Example 3

Append Student

```python
with open("students.txt", "a") as file:

    file.write("David\n")
```

---

# Practical Example 4

Copy File

```python
with open("source.txt", "r") as source:

    data = source.read()

with open("destination.txt", "w") as destination:

    destination.write(data)
```

---

# Practical Example 5

Count Number of Lines

```python
with open("sample.txt", "r") as file:

    count = 0

    for line in file:
        count += 1

print(count)
```

---

# 19. Common Interview Programs

### 1. Read Entire File

### 2. Read Line by Line

### 3. Count Number of Lines

### 4. Count Words

### 5. Count Characters

### 6. Copy One File to Another

### 7. Append Data

### 8. Search for a Word

### 9. Rename a File

### 10. Delete a File

### 11. Check File Exists

### 12. Merge Two Files

### 13. Read CSV File (Introduction)

### 14. Write Employee Records

### 15. Student Record Management

---

# 20. Common Errors

| Error | Reason |
|--------|--------|
| FileNotFoundError | File not found |
| PermissionError | No permission |
| FileExistsError | File already exists |
| IsADirectoryError | Directory opened as file |
| UnicodeDecodeError | Wrong file encoding |

---

# 21. Best Practices

- Always use `with open()`
- Close files properly
- Handle exceptions
- Use meaningful file names
- Check file existence before deleting
- Avoid overwriting important files

---

# 22. Quick Summary

| Function | Purpose |
|----------|---------|
| open() | Open a file |
| read() | Read entire file |
| readline() | Read one line |
| readlines() | Read all lines |
| write() | Write data |
| writelines() | Write multiple lines |
| close() | Close file |
| tell() | Current pointer position |
| seek() | Move pointer |
| os.rename() | Rename file |
| os.remove() | Delete file |

---

# Homework

1. Create a text file and write your name.
2. Read a file using `read()`.
3. Read a file line by line.
4. Append new data to a file.
5. Count the number of lines.
6. Count the number of words.
7. Count the number of characters.
8. Copy one file to another.
9. Rename a file.
10. Delete a file safely.

---

# Session Summary

Today we learned:

✔ File Handling

✔ File Modes

✔ Reading Files

✔ Writing Files

✔ Appending Data

✔ File Pointer

✔ tell()

✔ seek()

✔ with Statement

✔ Rename Files

✔ Delete Files

✔ Exception Handling with Files

✔ Practical File Programs

---

# Next Session Preview
