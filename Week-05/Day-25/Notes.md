# Python Full Stack Foundation

# Week-05 – Day-25

# Object-Oriented Programming (OOP)

# Advanced OOP Concepts in Python

**Level:** Beginner → Intermediate

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Encapsulation
- Understand Data Hiding
- Learn Name Mangling
- Use Getter and Setter Methods
- Understand @property
- Learn Class Variables
- Learn Instance Variables
- Learn Static Methods
- Learn Class Methods
- Understand Composition
- Differentiate Composition and Inheritance
- Learn Aggregation and Association
- Understand Abstraction
- Create Abstract Classes
- Understand Object Lifecycle
- Integrate all OOP concepts

---

# Recap

So far we have learned

✓ Classes

✓ Objects

✓ Constructors

✓ Methods

✓ self

✓ Inheritance

✓ Polymorphism

Today we complete Object-Oriented Programming.

---

# Complete OOP Pillars

```
Object-Oriented Programming

│

├── Encapsulation

├── Inheritance

├── Polymorphism

└── Abstraction
```

---

# What is Encapsulation?

## Definition

Encapsulation is the process of combining

- Data
- Methods

into a single unit (class) and restricting direct access to important data.

---

# Simple Definition

Protecting object data from direct modification.

---

# Real World Example

ATM Machine

You can

✔ Deposit Money

✔ Withdraw Money

✔ Check Balance

You cannot directly access

- Database
- PIN Records
- Bank Server

Everything is controlled.

This is Encapsulation.

---

# Why Encapsulation?

Suppose

```python
account.balance = -50000
```

Anyone can change balance.

This is unsafe.

Instead

```
Deposit()

Withdraw()

CheckBalance()
```

should control access.

---

# Access Levels in Python

Python has naming conventions.

| Type | Syntax | Meaning |
|------|---------|----------|
| Public | variable | Accessible everywhere |
| Protected | _variable | Internal use (convention) |
| Private | __variable | Name Mangling |

---

# Public Variable

```python
class Student:

    def __init__(self):

        self.name="Alex"

s=Student()

print(s.name)
```

Accessible anywhere.

---

# Protected Variable

```python
class Student:

    def __init__(self):

        self._marks=90
```

Convention

Developers understand

"Don't access directly."

Python still allows access.

---

# Private Variable

```python
class Student:

    def __init__(self):

        self.__salary=50000
```

Double underscore

creates Name Mangling.

---

# Name Mangling

Python changes

```
__salary
```

to

```
_Student__salary
```

internally.

This reduces accidental access.

---

# Example

```python
class Employee:

    def __init__(self):

        self.__salary=60000

e=Employee()

print(e.__salary)
```

Output

```
AttributeError
```

---

# Accessing Private Variable

```python
class Employee:

    def __init__(self):

        self.__salary=60000

    def display(self):

        print(self.__salary)

e=Employee()

e.display()
```

Output

```
60000
```

---

# Getter Methods

Definition

Getter methods read private variables.

Example

```python
class Employee:

    def __init__(self):

        self.__salary=50000

    def get_salary(self):

        return self.__salary

e=Employee()

print(e.get_salary())
```

---

# Setter Methods

Definition

Setter methods modify private variables safely.

Example

```python
class Employee:

    def __init__(self):

        self.__salary=50000

    def set_salary(self,value):

        if value>0:

            self.__salary=value

e=Employee()

e.set_salary(70000)

print(e.get_salary())
```

---

# Why Setter Methods?

Validation

```python
salary=-10000
```

Not allowed.

Setter prevents invalid values.

---

# @property

Python provides a cleaner way.

Instead of

```python
get_salary()
```

we write

```python
salary
```

---

# Example

```python
class Employee:

    def __init__(self):

        self.__salary=50000

    @property
    def salary(self):

        return self.__salary

e=Employee()

print(e.salary)
```

Notice

No brackets.

---

# Property Setter

```python
class Employee:

    def __init__(self):

        self.__salary=50000

    @property
    def salary(self):

        return self.__salary

    @salary.setter
    def salary(self,value):

        if value>0:

            self.__salary=value

e=Employee()

e.salary=70000

print(e.salary)
```

---

# Instance Variables

Definition

Variables belonging to each object.

Example

```python
class Student:

    def __init__(self,name):

        self.name=name
```

Every object has its own value.

---

# Class Variables

Definition

Variables shared by every object.

Example

```python
class Student:

    college="ABC College"

    def __init__(self,name):

        self.name=name
```

---

# Example

```python
s1=Student("Alex")

s2=Student("John")

print(s1.college)

print(s2.college)
```

Output

```
ABC College

ABC College
```

Only one copy exists.

---

# Instance Variable vs Class Variable

| Instance Variable | Class Variable |
|------------------|----------------|
| Unique for every object | Shared by all objects |
| Created using self | Created directly in class |
| Stored in object | Stored in class |

---

# Static Methods

Definition

A Static Method belongs to the class.

It does not access

- self
- cls

Used for utility functions.

---

# Example

```python
class Calculator:

    @staticmethod

    def add(a,b):

        return a+b

print(Calculator.add(10,20))
```

Output

```
30
```

---

# When to Use Static Methods

Examples

- Tax Calculation
- Unit Conversion
- Mathematical Utilities
- Validation Functions

---

# Class Methods

Definition

A Class Method works with the class itself.

Uses

```
cls
```

instead of

```
self
```

---

# Example

```python
class Student:

    college="ABC"

    @classmethod

    def change_college(cls,name):

        cls.college=name

Student.change_college("XYZ")

print(Student.college)
```

Output

```
XYZ
```

---

# Difference

| Method | First Parameter |
|---------|----------------|
| Instance Method | self |
| Class Method | cls |
| Static Method | None |

---

# Composition

## Definition

Composition means

One object contains another object.

HAS-A Relationship.

---

# Real World Example

Car

HAS-A

Engine

Student

HAS-A

Address

Computer

HAS-A

CPU

---

# Example

```python
class Address:

    def __init__(self,city):

        self.city=city


class Student:

    def __init__(self,name,address):

        self.name=name

        self.address=address


addr=Address("Hyderabad")

s=Student("Alex",addr)

print(s.address.city)
```

Output

```
Hyderabad
```

---

# Why Composition?

Separate responsibilities.

Student handles student details.

Address handles address details.

Cleaner design.

---

# Composition vs Inheritance

| Inheritance | Composition |
|-------------|-------------|
| IS-A | HAS-A |
| Dog IS-A Animal | Car HAS-A Engine |
| Reuse behaviour | Combine objects |

---

# Aggregation

Definition

Aggregation is a weak HAS-A relationship.

Objects can exist independently.

---

# Example

Teacher

↓

Department

Department exists

even if Teacher leaves.

---

# Association

Definition

Two independent objects communicate.

Example

Doctor

↓

Patient

Doctor exists independently.

Patient exists independently.

---

# Relationship Summary

| Relationship | Meaning |
|--------------|----------|
| Inheritance | IS-A |
| Composition | Strong HAS-A |
| Aggregation | Weak HAS-A |
| Association | Uses-A |

---

# Abstraction

## Definition

Abstraction means

Showing only essential features

while hiding implementation details.

---

# Real World Example

Car

Driver sees

✔ Steering

✔ Brake

✔ Accelerator

Hidden

✘ Engine Internals

✘ Fuel Injection

✘ Sensors

---

# Abstract Class

Python uses

```
abc
```

module.

---

# Example

```python
from abc import ABC,abstractmethod

class Shape(ABC):

    @abstractmethod

    def area(self):

        pass
```

Cannot create

```python
Shape()
```

Python raises

```
TypeError
```

---

# Child Class

```python
from abc import ABC,abstractmethod

class Shape(ABC):

    @abstractmethod

    def area(self):

        pass


class Rectangle(Shape):

    def __init__(self,l,w):

        self.l=l

        self.w=w

    def area(self):

        return self.l*self.w

r=Rectangle(10,5)

print(r.area())
```

Output

```
50
```

---

# Object Lifecycle

```
Object Creation

↓

Constructor

↓

Object Usage

↓

Garbage Collection

↓

Memory Released
```

---

# __new__()

Runs before

```
__init__()
```

Responsible for creating the object.

Normally

we do not override it.

---

# __del__()

Destructor

Executed when object is destroyed.

Example

```python
class Student:

    def __del__(self):

        print("Object Deleted")
```

Python automatically calls it

when the object is garbage collected.

---

# Complete OOP Flow

```
Create Class

↓

Create Object

↓

Constructor

↓

Methods

↓

Inheritance

↓

Polymorphism

↓

Encapsulation

↓

Composition

↓

Abstraction
```

---

# Mini Integration Example

```python
from abc import ABC,abstractmethod

class Person:

    college="ABC College"

    def __init__(self,name):

        self.name=name


class Student(Person):

    def __init__(self,name,marks):

        super().__init__(name)

        self.__marks=marks

    @property

    def marks(self):

        return self.__marks

    def display(self):

        print(self.name,self.__marks)
```

This example combines

✔ Constructor

✔ Inheritance

✔ Encapsulation

✔ Property

---

# Best Practices

✔ Use Inheritance only for IS-A relationships.

✔ Use Composition for HAS-A relationships.

✔ Keep data private whenever possible.

✔ Use @property instead of unnecessary getter methods.

✔ Use Static Methods for utility functions.

✔ Use Class Methods for class-wide changes.

✔ Keep classes focused on one responsibility.

---

# Common Mistakes

❌ Using inheritance everywhere.

❌ Making every variable public.

❌ Forgetting validation.

❌ Creating huge classes.

❌ Mixing unrelated responsibilities.

---

# Complete OOP Roadmap

```
Programming

↓

Classes

↓

Objects

↓

Attributes

↓

Methods

↓

Constructors

↓

Inheritance

↓

Polymorphism

↓

Encapsulation

↓

Composition

↓

Abstraction

↓

Projects
```

---

# Course Summary

During Week-05 you learned

✓ Classes

✓ Objects

✓ Attributes

✓ Methods

✓ self

✓ Constructors

✓ Instance Variables

✓ Inheritance

✓ super()

✓ Constructor Chaining

✓ Method Overriding

✓ Duck Typing

✓ Operator Overloading

✓ Magic Methods

✓ Encapsulation

✓ Properties

✓ Static Methods

✓ Class Methods

✓ Composition

✓ Aggregation

✓ Association

✓ Abstraction

✓ Abstract Classes

✓ Object Lifecycle

---

# What's Next?

You are now ready to build complete OOP applications such as:

- Student Management System
- Library Management System
- Banking System
- Hospital Management System
- Employee Payroll System
- E-Commerce Shopping Cart
- Hotel Reservation System
- Inventory Management System
- Vehicle Rental System
- Online Course Management System

These projects combine all the OOP concepts learned during Days 21–25.
