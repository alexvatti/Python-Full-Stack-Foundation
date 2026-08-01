````markdown
# Python OOP – Method Overriding, isinstance(), issubclass(), and Method Resolution Order (MRO)

## Learning Objectives

By the end of this lesson, you will be able to:

- Understand Method Overriding
- Differentiate between `isinstance()` and `issubclass()`
- Understand Method Resolution Order (MRO)
- View the MRO using `mro()` and `__mro__`

---

# 1. Method Overriding

## What is Method Overriding?

**Method Overriding** is an Object-Oriented Programming (OOP) concept where a **child class provides its own implementation of a method that already exists in the parent class**.

The child class **overrides** (replaces) the implementation of the parent class.

> **Method Overriding = Same Method Name + Same Parameters + Different Implementation**

---

## Why Do We Need Method Overriding?

Method overriding allows child classes to:

- Customize inherited behavior.
- Provide specialized implementations.
- Achieve Runtime Polymorphism.
- Reuse existing code while changing only the required functionality.

---

## Syntax

```python
class Parent:
    def display(self):
        print("Parent Method")


class Child(Parent):
    def display(self):
        print("Child Method")
```

---

# Example 1

```python
class Animal:
    def sound(self):
        print("Animals make different sounds")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


dog = Dog()
dog.sound()
```

### Output

```text
Dog barks
```

---

# Example 2

```python
class Vehicle:
    def start(self):
        print("Vehicle Started")


class Car(Vehicle):
    def start(self):
        print("Car Started")


car = Car()
car.start()
```

### Output

```text
Car Started
```

---

# Before Overriding

```python
class Animal:
    def sound(self):
        print("Generic Sound")


class Dog(Animal):
    pass


dog = Dog()
dog.sound()
```

### Output

```text
Generic Sound
```

The child class uses the parent's implementation because it does not define its own method.

---

# After Overriding

```python
class Animal:
    def sound(self):
        print("Generic Sound")


class Dog(Animal):
    def sound(self):
        print("Dog Barks")


dog = Dog()
dog.sound()
```

### Output

```text
Dog Barks
```

Now the child class replaces the parent's method.

---

# Method Overriding Rules

- Parent and child classes must have an inheritance relationship.
- Method name should be the same.
- Parameter list should usually be the same.
- Child implementation replaces the parent implementation.

---

# Real-World Examples

| Parent | Child | Overridden Method |
|---------|-------|-------------------|
| Animal | Dog | sound() |
| Vehicle | Car | start() |
| Employee | Manager | work() |
| Shape | Circle | draw() |
| Bird | Sparrow | fly() |

---

# Method Overriding vs Inheritance

| Inheritance | Method Overriding |
|-------------|-------------------|
| Child inherits methods | Child replaces inherited method |
| Code reuse | Customized behavior |
| Parent method available | Child method executed |

---

# Key Points

- Requires inheritance.
- Same method name.
- Same parameters.
- Different implementation.
- Supports Runtime Polymorphism.

---

# 2. isinstance() vs issubclass()

Both functions are related to classes, but they answer different questions.

| Function | Question |
|----------|----------|
| isinstance() | Is this object an instance of this class? |
| issubclass() | Is this class derived from another class? |

---

# isinstance()

## What?

Checks whether an **object** belongs to a class.

### Syntax

```python
isinstance(object, Class)
```

---

# Example 1

```python
class Animal:
    pass


class Dog(Animal):
    pass


dog = Dog()

print(isinstance(dog, Dog))
print(isinstance(dog, Animal))
```

### Output

```text
True
True
```

---

# Example 2

```python
class Vehicle:
    pass


class Car(Vehicle):
    pass


car = Car()

print(isinstance(car, Car))
print(isinstance(car, Vehicle))
print(isinstance(car, object))
```

### Output

```text
True
True
True
```

---

# Example 3

```python
number = 100

print(isinstance(number, int))
print(isinstance(number, float))
```

### Output

```text
True
False
```

---

# issubclass()

## What?

Checks whether one class inherits from another class.

### Syntax

```python
issubclass(ChildClass, ParentClass)
```

---

# Example 1

```python
class Animal:
    pass


class Dog(Animal):
    pass


print(issubclass(Dog, Animal))
print(issubclass(Animal, Dog))
```

### Output

```text
True
False
```

---

# Example 2

```python
class Vehicle:
    pass


class Car(Vehicle):
    pass


print(issubclass(Car, Vehicle))
print(issubclass(Car, object))
```

### Output

```text
True
True
```

---

# Example 3

```python
class LivingThing:
    pass


class Animal(LivingThing):
    pass


class Dog(Animal):
    pass


print(issubclass(Dog, LivingThing))
```

### Output

```text
True
```

---

# Common Mistakes

## Wrong

```python
dog = Dog()

issubclass(dog, Animal)
```

Output

```text
TypeError
```

Reason:

`issubclass()` expects **classes**, not objects.

---

## Wrong

```python
isinstance(Dog, Animal)
```

Output

```text
False
```

Reason:

`Dog` is a class, not an object.

---

# Comparison

| Feature | isinstance() | issubclass() |
|----------|--------------|--------------|
| Works With | Objects | Classes |
| Checks | Object Type | Class Hierarchy |
| Used For | Type Checking | Inheritance Checking |
| Returns | True / False | True / False |

---

# Easy Memory Trick

```text
instance → object

subclass → class
```

---

# 3. Method Resolution Order (MRO)

## What is MRO?

**Method Resolution Order (MRO)** is the order in which Python searches for methods and attributes in an inheritance hierarchy.

It becomes important in **multiple inheritance**, where multiple parent classes define the same method.

---

# Why Do We Need MRO?

Suppose two parent classes contain the same method.

Which method should Python execute?

Python follows the **Method Resolution Order (MRO)** to decide.

---

# Example 1

```python
class A:
    def display(self):
        print("Class A")


class B(A):
    def display(self):
        print("Class B")


class C(A):
    def display(self):
        print("Class C")


class D(B, C):
    pass


obj = D()
obj.display()
```

### Output

```text
Class B
```

---

# How Python Searches

Python checks in this order:

```text
D
↓
B
↓
C
↓
A
↓
object
```

The method is found in **B**, so Python stops searching.

---

# Example 2

```python
class Printer:
    def print_data(self):
        print("Printer")


class Scanner:
    def print_data(self):
        print("Scanner")


class AllInOne(Printer, Scanner):
    pass


device = AllInOne()

device.print_data()
```

### Output

```text
Printer
```

Python searches:

```text
AllInOne
↓

Printer ✅
↓

Scanner
↓

object
```

---

# Viewing the MRO

## Method 1

```python
print(D.mro())
```

Output

```text
[<class '__main__.D'>,
<class '__main__.B'>,
<class '__main__.C'>,
<class '__main__.A'>,
<class 'object'>]
```

---

## Method 2

```python
print(D.__mro__)
```

Output

```text
(<class '__main__.D'>,
<class '__main__.B'>,
<class '__main__.C'>,
<class '__main__.A'>,
<class 'object'>)
```

---

# Difference

| Method | Returns |
|----------|----------|
| mro() | List |
| __mro__ | Tuple |

Both return the same search order.

---

# MRO Rules

- Starts with the current class.
- Searches parent classes from left to right.
- Stops when the method is found.
- Every class ultimately inherits from `object`.
- Python uses the **C3 Linearization Algorithm** to compute the MRO.

---

# Why MRO Matters

Without MRO, Python would not know which method to execute when multiple parent classes contain methods with the same name.

MRO guarantees:

- Predictable behavior
- No ambiguity
- Consistent method lookup

---

# Summary

| Topic | Purpose |
|---------|----------|
| Method Overriding | Replace parent method in child class |
| isinstance() | Check whether an object belongs to a class |
| issubclass() | Check whether one class inherits from another |
| MRO | Decide the order of method lookup |

---

# Interview Questions

### Q1. What is Method Overriding?

A child class provides its own implementation of a parent class method.

---

### Q2. Difference between isinstance() and issubclass()?

- `isinstance()` works with objects.
- `issubclass()` works with classes.

---

### Q3. What is MRO?

The order in which Python searches for methods in an inheritance hierarchy.

---

### Q4. How do you view the MRO?

```python
ClassName.mro()

ClassName.__mro__
```

---

### Q5. Why is MRO required?

To resolve ambiguity in multiple inheritance when multiple parent classes contain methods with the same name.

---

# Key Takeaways

- Method Overriding allows child classes to customize inherited methods.
- `isinstance()` checks **objects**, while `issubclass()` checks **classes**.
- MRO determines the order in which Python searches for methods.
- Python follows the **C3 Linearization Algorithm** for MRO.
- Use `ClassName.mro()` or `ClassName.__mro__` to inspect the method lookup order.
````
