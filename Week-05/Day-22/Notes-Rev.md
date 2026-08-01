# Python OOP: Variables & Methods

A study guide covering access modifiers, variable scope, and method types in Python classes.

---

## 1. Access Modifiers

Python doesn't enforce access control the way Java or C++ do — these are **conventions**, not hard restrictions (except name mangling, which adds a mild technical barrier).

### 1.1 Public Variable

**What:** Accessible from anywhere — inside the class, outside the class, from subclasses.
**Why it matters:** Used for data that's meant to be freely read or modified. It's the default in Python — no special syntax needed.

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner      # public
        self.balance = balance  # public

acc = Account("Alex", 1000)
print(acc.balance)   # 1000 — accessible directly
acc.balance = 1500    # modifiable directly
```

### 1.2 Protected Variable

**What:** Prefixed with a single underscore (`_variable`). A convention signaling "internal use — don't touch this from outside unless you know what you're doing."
**Why it matters:** Discourages accidental external access without actually blocking it. Subclasses are expected to use protected members; outside code is expected to leave them alone.

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self._balance = balance  # protected — internal convention

class SavingsAccount(Account):
    def add_interest(self, rate):
        self._balance += self._balance * rate  # subclass can access it

acc = SavingsAccount("Alex", 1000)
acc.add_interest(0.05)
print(acc._balance)  # 1050 — still technically accessible, but you're "not supposed to"
```

### 1.3 Private Variable

**What:** Prefixed with a double underscore (`__variable`). Python performs **name mangling**, rewriting `__balance` to `_ClassName__balance` internally.
**Why it matters:** Protects sensitive implementation details from accidental access or naming collisions in subclasses — it's the closest Python gets to true "private."

```python
class Account:
    def __init__(self, owner, balance):
        self.owner = owner
        self.__balance = balance  # private — name-mangled

    def get_balance(self):
        return self.__balance

acc = Account("Alex", 1000)
print(acc.get_balance())    # 1000 — access via a method
# print(acc.__balance)      # AttributeError
print(acc._Account__balance)  # 1000 — still reachable if you know the mangled name
```

---

## 2. Variable Scope

### 2.1 Instance Variable

**What:** Belongs to a single object. Each instance keeps its own separate copy, usually defined in `__init__` using `self`.
**Why it matters:** Every object maintains its own independent state — changing one object's data doesn't affect another's.

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name        # instance variable
        self.salary = salary    # instance variable

e1 = Employee("Priya", 50000)
e2 = Employee("Rahul", 60000)

e1.salary = 55000
print(e1.salary, e2.salary)  # 55000 60000 — independent copies
```

### 2.2 Class Variable

**What:** Belongs to the class itself, shared across all instances. Defined directly inside the class body, outside any method.
**Why it matters:** Saves memory (one copy instead of many) and is useful for data that should be consistent across every object — like a company name or a counter.

```python
class Employee:
    company_name = "Magnetpreneur"  # class variable — shared by all
    employee_count = 0

    def __init__(self, name):
        self.name = name              # instance variable
        Employee.employee_count += 1  # updates the shared value

e1 = Employee("Priya")
e2 = Employee("Rahul")

print(e1.company_name, e2.company_name)  # both see "Magnetpreneur"
print(Employee.employee_count)           # 2 — shared across all instances
```

---

## 3. Method Types

### 3.1 Instance Method

**What:** The default method type. Takes `self` as its first parameter, giving it access to the calling object's instance data.
**Why it matters:** This is how objects work with — and modify — their own specific data.

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):              # instance method — uses self
        return 3.14159 * self.radius ** 2

c = Circle(5)
print(c.area())  # 78.53975 — works with this object's own radius
```

### 3.2 Class Method

**What:** Decorated with `@classmethod`, takes `cls` as its first parameter instead of `self`. Operates on the class itself, not a specific instance.
**Why it matters:** Useful for working with class-wide data, or for creating alternative constructors that build objects in different ways.

```python
class Circle:
    total_circles = 0

    def __init__(self, radius):
        self.radius = radius
        Circle.total_circles += 1

    @classmethod
    def from_diameter(cls, diameter):   # class method — alternative constructor
        return cls(diameter / 2)

    @classmethod
    def count(cls):
        return cls.total_circles

c1 = Circle(5)
c2 = Circle.from_diameter(10)  # creates a Circle with radius 5
print(Circle.count())          # 2 — works with class-wide data
```

### 3.3 Static Method

**What:** Decorated with `@staticmethod`. Takes neither `self` nor `cls` — behaves like a regular function that just happens to live inside the class.
**Why it matters:** Groups related utility functions inside the class for organization, even when they don't need access to instance or class data.

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

    @staticmethod
    def is_valid_radius(value):   # static method — no self, no cls
        return value > 0

print(Circle.is_valid_radius(5))   # True
print(Circle.is_valid_radius(-2))  # False — pure utility check, no object needed
```

---

## Quick Reference

| Concept | What | Why It Matters |
|---|---|---|
| Public Variable | Accessible everywhere | Data anyone can read/modify safely |
| Protected Variable | Internal-use convention (`_var`) | Discourages accidental external access |
| Private Variable | Name-mangled variable (`__var`) | Protects sensitive implementation details |
| Instance Variable | One copy per object | Every object maintains its own state |
| Class Variable | One copy for all objects | Saves memory, stores shared information |
| Instance Method | Uses `self` | Works with object-specific data |
| Class Method | Uses `cls` | Works with class-wide shared data |
| Static Method | Uses neither `self` nor `cls` | Groups related utility functions in the class |
