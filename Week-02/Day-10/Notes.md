# Python Full Stack Foundation

# Week 2 – Day 10

## while Loop, break, continue, pass, Collections & Common Methods

---

# Learning Objectives

By the end of this session, learners will be able to:

* Understand while Loop
* Use break Statement
* Use continue Statement
* Use pass Statement
* Understand Infinite Loops
* Work with Lists, Tuples, Sets, Dictionaries, and Strings
* Use Common Collection Methods
* Build Menu-Driven Programs

---

# Recap

Previously we learned:

* for Loop
* range()
* Loop Patterns
* Iterating through Collections

Today we will learn:

```text
while Loop
break
continue
pass

and

Important Collection Methods
```

---

# 1. Collections Overview

Before learning while loop, let's revisit Python collections.

| Collection | Symbol | Ordered | Mutable |
| ---------- | ------ | ------- | ------- |
| List       | []     | Yes     | Yes     |
| Tuple      | ()     | Yes     | No      |
| Set        | {}     | No      | Yes     |
| Dictionary | {}     | Yes     | Yes     |
| String     | ""     | Yes     | No      |

---

# List

Stores multiple values.

```python
subjects = ["Python", "SQL", "HTML"]
```

---

# Common List Methods

## append()

Add item at end.

```python
subjects = ["Python", "SQL"]

subjects.append("HTML")

print(subjects)
```

Output

```text
['Python', 'SQL', 'HTML']
```

---

## insert()

```python
subjects.insert(1, "Java")
```

Output

```text
['Python', 'Java', 'SQL']
```

---

## remove()

```python
subjects.remove("SQL")
```

---

## pop()

```python
subjects.pop()
```

Removes last item.

---

## sort()

```python
nums = [5,1,3,2]

nums.sort()

print(nums)
```

Output

```text
[1,2,3,5]
```

---

## reverse()

```python
nums.reverse()
```

---

## len()

```python
print(len(subjects))
```

---

# Tuple

Immutable collection.

```python
subjects = ("Python","SQL","HTML")
```

---

# Common Tuple Methods

## count()

```python
data = (10,20,10,30)

print(data.count(10))
```

Output

```text
2
```

---

## index()

```python
print(data.index(20))
```

Output

```text
1
```

---

# Set

Stores unique values.

```python
skills = {"Python","SQL","Python"}
```

Output

```text
{'Python','SQL'}
```

Duplicate removed.

---

# Common Set Methods

## add()

```python
skills.add("HTML")
```

---

## remove()

```python
skills.remove("SQL")
```

---

## union()

```python
a = {1,2}
b = {2,3}

print(a.union(b))
```

Output

```text
{1,2,3}
```

---

## intersection()

```python
print(a.intersection(b))
```

Output

```text
{2}
```

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

# Common Dictionary Methods

## keys()

```python
print(student.keys())
```

---

## values()

```python
print(student.values())
```

---

## items()

```python
print(student.items())
```

---

## get()

```python
print(student.get("name"))
```

Output

```text
Alex
```

---

## update()

```python
student.update({"age":25})
```

---

## pop()

```python
student.pop("city")
```

---

# String

Collection of characters.

```python
name = "Python"
```

---

# Common String Methods

## upper()

```python
print(name.upper())
```

Output

```text
PYTHON
```

---

## lower()

```python
print(name.lower())
```

Output

```text
python
```

---

## replace()

```python
print(name.replace("Python","Java"))
```

Output

```text
Java
```

---

## split()

```python
text = "Python SQL HTML"

print(text.split())
```

Output

```text
['Python','SQL','HTML']
```

---

## strip()

```python
text = " Python "

print(text.strip())
```

---

# Summary of Important Methods

| Collection | Important Methods                          |
| ---------- | ------------------------------------------ |
| List       | append, insert, remove, pop, sort, reverse |
| Tuple      | count, index                               |
| Set        | add, remove, union, intersection           |
| Dictionary | keys, values, items, get, update           |
| String     | upper, lower, replace, split, strip        |

---

# 2. What is a while Loop?

A while loop executes as long as a condition remains True.

---

# Syntax

```python
while condition:
    statements
```

---

# Flow

```text
Condition
    |
 True
    |
 Execute
    |
 Go Back

False
    |
 Stop
```

---

# Example 1

```python
i = 1

while i <= 5:
    print(i)
    i += 1
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

Continue until:

```text
i = 6
```

Condition becomes False.

---

# Example 2

Print Hello 5 Times

```python
count = 1

while count <= 5:
    print("Hello")
    count += 1
```

---

# Example 3

Print Even Numbers

```python
num = 2

while num <= 10:
    print(num)
    num += 2
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

# Example 4

Print Odd Numbers

```python
num = 1

while num <= 10:
    print(num)
    num += 2
```

---

# Example 5

Multiplication Table

```python
num = 5
i = 1

while i <= 10:
    print(f"{num} x {i} = {num*i}")
    i += 1
```

---

# Infinite Loop

```python
while True:
    print("Python")
```

Runs forever.

---

# Common Mistake

```python
i = 1

while i <= 5:
    print(i)
```

Output

```text
Infinite Loop
```

Reason:

```text
i never changes
```

---

# 3. break Statement

Used to terminate the loop immediately.

---

# Example

```python
i = 1

while i <= 10:

    if i == 5:
        break

    print(i)
    i += 1
```

Output

```text
1
2
3
4
```

---

# Real World Example

ATM Exit Option

```python
while True:

    choice = input("Enter Option: ")

    if choice == "exit":
        break

    print("Processing...")
```

---

# 4. continue Statement

Skip current iteration.

---

# Example

```python
for i in range(1,6):

    if i == 3:
        continue

    print(i)
```

Output

```text
1
2
4
5
```

---

# Example Using while

```python
i = 0

while i < 5:

    i += 1

    if i == 3:
        continue

    print(i)
```

Output

```text
1
2
4
5
```

---

# Use Case

Skip absent students.

```python
students = ["Alex","John","Mary"]

for student in students:

    if student == "John":
        continue

    print(student)
```

---

# 5. pass Statement

Used as a placeholder.

---

# Example

```python
if True:
    pass
```

Program runs successfully.

---

# Why pass?

Suppose you want to write code later.

```python
if age >= 18:
    pass
```

---

# Example

```python
for i in range(5):
    pass
```

No error.

---

# Difference

| Statement | Meaning        |
| --------- | -------------- |
| break     | Exit Loop      |
| continue  | Skip Iteration |
| pass      | Do Nothing     |

---

# Menu Driven Program

```python
while True:

    print("1. Add")
    print("2. View")
    print("3. Exit")

    choice = input("Enter Choice: ")

    if choice == "1":
        print("Adding")

    elif choice == "2":
        print("Viewing")

    elif choice == "3":
        print("Good Bye")
        break

    else:
        print("Invalid Choice")
```

---

# Collection Iteration Using while

## List

```python
subjects = ["Python","SQL","HTML"]

i = 0

while i < len(subjects):
    print(subjects[i])
    i += 1
```

---

## Tuple

```python
data = (10,20,30)

i = 0

while i < len(data):
    print(data[i])
    i += 1
```

---

## String

```python
name = "Python"

i = 0

while i < len(name):
    print(name[i])
    i += 1
```

---

## Dictionary

```python
student = {
    "name":"Alex",
    "city":"Hyderabad"
}

for key in student:
    print(key, student[key])
```

---

# Mini Project 1

Password Checker

```python
password = ""

while password != "admin123":
    password = input("Enter Password: ")

print("Login Successful")
```

---

# Mini Project 2

Number Guessing

```python
secret = 7

while True:

    num = int(input("Guess: "))

    if num == secret:
        print("Correct")
        break
```

---

# Quick Summary

| Topic    | Purpose                       |
| -------- | ----------------------------- |
| while    | Repetition based on condition |
| break    | Exit loop                     |
| continue | Skip iteration                |
| pass     | Placeholder                   |
| append() | Add item to list              |
| add()    | Add item to set               |
| get()    | Read dictionary value         |
| upper()  | Convert string to uppercase   |

---

# Session Summary

Today we learned:

✔ List Methods

✔ Tuple Methods

✔ Set Methods

✔ Dictionary Methods

✔ String Methods

✔ while Loop

✔ Infinite Loop

✔ break

✔ continue

✔ pass

✔ Menu Driven Programs

✔ Collection Traversal

---

# Homework

1. Print 1 to 100 using while.
2. Print Even Numbers using while.
3. Print Odd Numbers using while.
4. Create Multiplication Table using while.
5. Create Login Validation Program.
6. Create Number Guessing Program.
7. Practice break examples.
8. Practice continue examples.
9. Practice pass examples.
10. Practice all collection methods.

---

# Week 2 Completed 🎉

You can now:

✔ Make Decisions

✔ Use if, if-else, if-elif-else

✔ Create Nested Conditions

✔ Use for Loops

✔ Use while Loops

✔ Work with Collections

✔ Control Loop Execution using break, continue, and pass

✔ Build Menu-Driven Programs

---

# Next Session Preview

## Week 3 – Day 11

* Functions
* Function Definition
* Function Calling
* Return Values
* Code Reusability

Get ready to write reusable and organized Python programs.
