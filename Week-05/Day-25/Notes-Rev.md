````markdown
# OOP Relationships in Python

One of the most common areas of confusion in OOP is deciding **which relationship to use** between classes.

There are four major relationships:

| Relationship | Meaning | Ownership | Lifetime |
|-------------|----------|-----------|----------|
| Inheritance | **IS-A** | No ownership | Independent |
| Composition | **Strong HAS-A** | Strong ownership | Dependent |
| Aggregation | **Weak HAS-A** | Weak ownership | Independent |
| Association | **USES-A / WORKS-WITH** | No ownership | Independent |

---

# 1. Inheritance (IS-A)

## What?

Inheritance represents an **IS-A** relationship.

The child class **is a specialized version** of the parent class.

### Ask Yourself

> **Is this object a type of another object?**

If the answer is **YES**, use **Inheritance**.

---

## Real-World Examples

- Dog **is an** Animal
- Car **is a** Vehicle
- Student **is a** Person
- Manager **is an** Employee

---

## Python Example

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")


dog = Dog()

dog.eat()
dog.bark()
```

### Diagram

```text
Animal
   ↑
   │
 Dog
```

---

## Why?

A Dog **is an Animal**.

The child gets all the behavior of the parent.

---

# 2. Composition (Strong HAS-A)

## What?

Composition represents a **Strong HAS-A** relationship.

One object **owns** another object.

The owned object **cannot normally exist without its owner**.

---

## Ask Yourself

> **Does this object own another object?**

If **YES**, Composition is appropriate.

---

## Real-World Examples

- House has Rooms
- Human has Heart
- Car has Engine
- Mobile has Battery

---

## Important Characteristic

If the owner is destroyed,

the owned object is also destroyed.

---

## Python Example

```python
class Engine:
    def start(self):
        print("Engine Started")


class Car:

    def __init__(self):
        self.engine = Engine()

    def drive(self):
        self.engine.start()
        print("Car Moving")


car = Car()

car.drive()
```

### Output

```text
Engine Started
Car Moving
```

---

## Diagram

```text
Car
 │
 └── Engine
```

---

## Why Composition?

The engine belongs to that specific car.

The car creates and manages the engine.

---

# 3. Aggregation (Weak HAS-A)

## What?

Aggregation is also a **HAS-A** relationship,

but ownership is **weak**.

The contained object **can exist independently**.

---

## Ask Yourself

> **Does this object simply contain or use another object that can live on its own?**

If YES,

use Aggregation.

---

## Real-World Examples

- Department has Employees
- Library has Books
- School has Teachers
- Team has Players

Employees, books, teachers, and players all exist independently.

---

## Python Example

```python
class Employee:

    def __init__(self, name):
        self.name = name


class Department:

    def __init__(self, employee):
        self.employee = employee

    def show(self):
        print(self.employee.name)


emp = Employee("Alex")

dept = Department(emp)

dept.show()
```

### Output

```text
Alex
```

---

## Diagram

```text
Department
      │
      │
Employee
```

---

## Why Aggregation?

The employee existed **before** joining the department.

If the department closes,

the employee still exists.

---

# 4. Association (USES-A)

## What?

Association is the weakest relationship.

One object **uses another object**.

Neither object owns the other.

---

## Ask Yourself

> **Does one object simply interact with another?**

If YES,

use Association.

---

## Real-World Examples

- Doctor treats Patient
- Customer places Order
- Teacher teaches Student
- Driver drives Car

Both objects exist independently.

---

## Python Example

```python
class Customer:

    def __init__(self, name):
        self.name = name


class Order:

    def place_order(self, customer):
        print(customer.name, "placed an order")


customer = Customer("Alex")

order = Order()

order.place_order(customer)
```

### Output

```text
Alex placed an order
```

---

## Diagram

```text
Customer  ─────────►  Order
```

---

## Why Association?

The order only **uses** the customer object.

It doesn't own it.

The customer continues to exist even after placing the order.

---

# Composition vs Aggregation

This is where most beginners get confused.

---

## Example 1 — Composition

```python
class Engine:
    pass


class Car:

    def __init__(self):
        self.engine = Engine()
```

Question:

**Who creates the engine?**

Answer:

The Car.

If the car is destroyed,

its engine is also destroyed.

**Strong ownership**

---

## Example 2 — Aggregation

```python
class Engine:
    pass


class Car:

    def __init__(self, engine):
        self.engine = engine


engine = Engine()

car = Car(engine)
```

Question:

Who creates the engine?

Answer:

Someone else.

The Car only receives it.

The engine continues to exist without the car.

**Weak ownership**

---

# Composition vs Association

Composition

```python
class Car:

    def __init__(self):
        self.engine = Engine()
```

Car **owns** Engine.

---

Association

```python
class Driver:

    def drive(self, car):
        print("Driving")
```

Driver only **uses** the Car.

Driver does not own the Car.

---

# Aggregation vs Association

Aggregation

```text
Department HAS-A Employee
```

The department stores employees.

---

Association

```text
Doctor USES-A Patient
```

Doctor interacts with patient.

No ownership.

---

# Complete Comparison

| Feature | Inheritance | Composition | Aggregation | Association |
|----------|-------------|-------------|-------------|-------------|
| Meaning | IS-A | Strong HAS-A | Weak HAS-A | USES-A |
| Ownership | No | Strong | Weak | None |
| Lifetime | Independent | Dependent | Independent | Independent |
| Object Creation | Parent/Child | Owner creates object | External object passed | External object used |
| Code Reuse | Yes | No | No | No |
| Flexibility | Medium | High | High | Highest |

---

# Which Relationship Should You Choose?

```text
Is it a type of another object?

YES
 ↓
Inheritance
```

```text
Does it own another object?

YES
 ↓
Composition
```

```text
Does it simply contain an existing object?

YES
 ↓
Aggregation
```

```text
Does it only interact with another object?

YES
 ↓
Association
```

---

# Easy Memory Trick

```text
IS-A
↓

Inheritance
```

```text
HAS-A and owns it
↓

Composition
```

```text
HAS-A but doesn't own it
↓

Aggregation
```

```text
Just works with it
↓

Association
```

---

# Interview Questions

### Q1. What is the difference between Composition and Aggregation?

**Composition** has strong ownership—the owner creates and controls the object's lifetime.

**Aggregation** has weak ownership—the contained object exists independently and is simply referenced.

---

### Q2. When should you use Inheritance?

Use inheritance only when there is a genuine **IS-A** relationship.

Example:

- Dog is an Animal ✅
- Car is a Vehicle ✅
- Car is an Engine ❌

---

### Q3. Which relationship is preferred in modern Python?

Prefer **Composition over Inheritance** unless there is a clear **IS-A** relationship. Composition usually results in more flexible and maintainable designs.
````
