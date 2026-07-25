# Python Full Stack Foundation

# Week-05 – Day-21

# Object-Oriented Programming (OOP)

## Classes, Objects and OOP Fundamentals

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Object-Oriented Programming (OOP)
- Explain why OOP is used
- Compare Procedural Programming with OOP
- Create Classes
- Create Objects
- Understand Attributes
- Create Multiple Objects
- Visualize how objects are stored in memory
- Build simple real-world classes

---

# What is Programming?

Programming is the process of writing instructions that tell a computer how to solve a problem or perform a task.

Example:

```python
print("Hello World")
```

The computer executes instructions one by one.

---

# What is a Program?

A Program is a collection of instructions written in a programming language.

Example

```
Take Input
↓

Process Data

↓

Display Output
```

---

# Different Programming Paradigms

Programming languages support different styles of programming.

Some common paradigms are

- Procedural Programming
- Object-Oriented Programming (OOP)
- Functional Programming
- Event Driven Programming

Python supports all of these, but one of its biggest strengths is Object-Oriented Programming.

---

# What is Object-Oriented Programming (OOP)?

## Definition

Object-Oriented Programming (OOP) is a programming paradigm that organizes a program into **objects**, where each object contains:

- Data (Attributes)
- Behaviour (Methods)

Instead of writing only functions, we model real-world entities as objects.

---

# Simple Definition

Think about the real world.

Everything around us is an object.

Examples

- Student
- Car
- Mobile Phone
- Laptop
- Employee
- Book
- Hospital Patient
- Bank Account

Every object has

- Characteristics (Properties)
- Actions (Behaviour)

---

# Real World Example

## Car

Properties

- Brand
- Model
- Colour
- Speed
- Fuel Type

Behaviour

- Start()
- Stop()
- Brake()
- Accelerate()

---

## Student

Properties

- Roll Number
- Name
- Age
- Department
- Marks

Behaviour

- Study()
- AttendClass()
- WriteExam()
- DisplayDetails()

---

## Bank Account

Properties

- Account Number
- Holder Name
- Balance

Behaviour

- Deposit()
- Withdraw()
- CheckBalance()

Notice that every real-world object contains both information and actions.

OOP follows the same concept.

---

# Why was OOP Introduced?

Imagine building software for a college.

There are

- 5 Students
- 20 Teachers
- 100 Courses
- 500 Books

If we use only variables and functions, the program quickly becomes difficult to manage.

Example

```python
student1_name = "Alex"
student1_marks = 90

student2_name = "John"
student2_marks = 88

student3_name = "David"
student3_marks = 76
```

As the number of students increases, the code becomes repetitive.

---

Now imagine storing everything inside one object.

```
Student

↓

Name

Roll No

Marks

Department

Study()

Display()
```

Everything related to a student stays together.

---

# Advantages of OOP

## 1. Code Reusability

Write once.

Reuse many times.

---

## 2. Better Organization

Data and functions stay together.

---

## 3. Easy Maintenance

Changes can be made in one place.

---

## 4. Easy Debugging

Since each object has its own responsibility, locating bugs becomes easier.

---

## 5. Real World Modelling

OOP closely matches how we think about real-world entities.

---

## 6. Scalability

Large applications become easier to expand.

Examples

- Hospital Management
- Banking System
- College ERP
- Shopping Website
- Flight Reservation

---

# Procedural Programming

Procedural Programming focuses on functions.

Example

```python
name = "Alex"
marks = 90

def display():
    print(name, marks)

display()
```

The data exists outside the function.

---

# Object-Oriented Programming

In OOP, data belongs to the object.

```python
class Student:

    def display(self):
        print(self.name)
```

The object stores both

- Data
- Behaviour

---

# Procedural Programming vs OOP

| Procedural Programming | Object-Oriented Programming |
|------------------------|-----------------------------|
| Functions are primary | Objects are primary |
| Data is separate | Data belongs to objects |
| Less reusable | Highly reusable |
| Hard to maintain | Easy to maintain |
| Suitable for small projects | Suitable for large projects |

---

# What is a Class?

## Definition

A Class is a blueprint used to create objects.

It defines

- What data an object should have.
- What actions an object can perform.

---

# Real World Analogy

Blueprint

↓

House

Blueprint

↓

Many Houses

Similarly

Class

↓

Many Objects

---

# More Examples

Blueprint

↓

Car Factory

↓

Creates many cars

Similarly

```
Student Class

↓

Student Object 1

Student Object 2

Student Object 3
```

One class can create any number of objects.

---

# Python Syntax

```python
class Student:
    pass
```

---

# Understanding the Syntax

```python
class Student:
    pass
```

### class

Keyword used to create a class.

---

### Student

Class Name

By convention, class names use PascalCase.

Examples

```python
class BankAccount:
    pass

class Employee:
    pass

class ShoppingCart:
    pass
```

---

### pass

A placeholder statement.

Python expects some code inside the class.

If nothing is written, we use

```python
pass
```

---

# What is an Object?

## Definition

An Object is an instance of a class.

The class is only a blueprint.

The object is the actual entity created from that blueprint.

---

# Real World Example

Blueprint

↓

House

Blueprint = Class

House = Object

---

Another Example

Student Class

↓

Alex

↓

John

↓

David

Each student is an object.

---

# Creating an Object

```python
class Student:
    pass

s1 = Student()
```

Student() creates a new object.

The variable s1 stores a reference to that object.

---

# Memory Representation

```
RAM

+----------------------+
| Student Object       |
|                      |
|                      |
+----------------------+

          ▲
          │
         s1
```

The object is stored in memory.

The variable only refers to its location.

---

# Creating Multiple Objects

```python
class Student:
    pass

s1 = Student()
s2 = Student()
s3 = Student()
```

Memory

```
s1 ─────► Object 1

s2 ─────► Object 2

s3 ─────► Object 3
```

Each object has its own memory.

Changing one object does not affect another.

---

# Example

```python
class Student:
    pass

student1 = Student()
student2 = Student()

print(student1)

print(student2)
```

Sample Output

```
<__main__.Student object at 0x...>

<__main__.Student object at 0x...>
```

Notice

The memory addresses are different.

Each object is unique.

---

# Summary

In this lesson, we learned

✓ What Programming is

✓ What OOP is

✓ Why OOP is important

✓ Advantages of OOP

✓ Procedural vs OOP

✓ Class

✓ Object

✓ Creating Objects

✓ Creating Multiple Objects

---

## Coming Next (Day-22 )

- Attributes
- Dynamic Attributes
- Instance Variables
- Object Identity (`id()`)
- `__dict__`
- Object Memory
- Multiple Real-World Examples
- Student Management System (Part 1)
