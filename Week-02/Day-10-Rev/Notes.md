# Week-02 Day-10 — Python Dictionaries
### Complete Theory, Syntax, Code Examples & Interview Programs

---

## Table of Contents

1. [Theory & Introduction](#1-theory--introduction)
2. [Syntax & Creation](#2-syntax--creation)
3. [Accessing Values](#3-accessing-values)
4. [Adding & Updating Elements](#4-adding--updating-elements)
5. [Deleting Elements](#5-deleting-elements)
6. [Mathematical Operators](#6-mathematical-operators)
7. [Membership Operators](#7-membership-operators)
8. [Comparison Operators](#8-comparison-operators)
9. [Built-in Functions](#9-built-in-functions)
10. [Iteration — keys, values, items](#10-iteration--keys-values-items)
11. [Dictionary Methods](#11-dictionary-methods)
12. [Dictionary Comprehension](#12-dictionary-comprehension)
13. [Nested Dictionaries](#13-nested-dictionaries)
14. [Dictionary vs List vs Set vs Tuple](#14-dictionary-vs-list-vs-set-vs-tuple)
15. [15 Interview Programs](#15-15-interview-programs)
16. [Summary](#16-summary)
17. [Self-Study Exercises](#17-self-study-exercises)

---

## 1. Theory & Introduction

### What is a Dictionary?

A **dictionary** is an **ordered** (Python 3.7+), **mutable** collection of **key-value pairs**. Each key maps to exactly one value. Dictionaries are the most important data structure in Python after lists — they power Python's own object system under the hood.

Also known in other languages as: **hash map**, **hash table**, **associative array**, **map**.

### Key Characteristics

| Property | Description |
|----------|-------------|
| **Ordered** | Insertion order is preserved (Python 3.7+) |
| **Mutable** | Keys/values can be added, changed, or removed |
| **Key-Value Pairs** | Every element is a pair: `key: value` |
| **Unique Keys** | Duplicate keys not allowed — later value overwrites earlier |
| **Keys Must Be Hashable** | Keys must be immutable (str, int, float, tuple) |
| **Values Can Be Anything** | Values can be any Python object |
| **Fast Lookup** | Key lookup is O(1) — hash table internally |

### Internal Working (Hash Table)

```
d = {"name": "Alex", "age": 30, "city": "Hyderabad"}

Internally (simplified):
  hash("name") → slot 4 → "Alex"
  hash("age")  → slot 7 → 30
  hash("city") → slot 2 → "Hyderabad"

d["age"] → compute hash("age") → go to slot 7 → return 30  ← O(1)
```

### Real-World Analogies

| Dictionary | Real-World Equivalent |
|------------|----------------------|
| `{"name": "Alex"}` | Contact book: name → phone number |
| `{"INR": 83.5}` | Currency table: currency code → rate |
| `{"A": 4.0}` | Grade lookup: letter → GPA points |
| `{1: "Jan"}` | Calendar: month number → name |

---

## 2. Syntax & Creation

```python
# Empty dictionary
d1 = {}
d2 = dict()
print(type(d1))             # <class 'dict'>
print(type(d2))             # <class 'dict'>

# Key-value pairs with curly braces
student = {"name": "Alex", "age": 25, "city": "Hyderabad"}
print(student)

# Using dict() constructor with keyword arguments
person = dict(name="Bob", age=30, city="Delhi")
print(person)

# Using dict() with list of tuples
pairs = dict([("a", 1), ("b", 2), ("c", 3)])
print(pairs)                # {'a': 1, 'b': 2, 'c': 3}

# Using dict() with zip
keys   = ["name", "age", "score"]
values = ["Alice", 22, 95.5]
d3 = dict(zip(keys, values))
print(d3)                   # {'name': 'Alice', 'age': 22, 'score': 95.5}

# Heterogeneous keys and values
mixed = {1: "one", "two": 2, (3, 4): "tuple_key", "list_val": [1, 2, 3]}
print(mixed)

# Duplicate keys — last value wins
d4 = {"a": 1, "b": 2, "a": 99}
print(d4)                   # {'a': 99, 'b': 2}

# Nested dictionary
nested = {
    "student": {"name": "Alex", "grade": "A"},
    "scores":  {"math": 95, "science": 88}
}
print(nested)

# fromkeys() — create dict with default value
keys_list = ["a", "b", "c", "d"]
d5 = dict.fromkeys(keys_list, 0)
print(d5)                   # {'a': 0, 'b': 0, 'c': 0, 'd': 0}

d6 = dict.fromkeys(["x", "y", "z"])    # Default value is None
print(d6)                   # {'x': None, 'y': None, 'z': None}

# What CANNOT be a key
try:
    bad = {[1, 2]: "list key"}  # list is unhashable
except TypeError as e:
    print(f"Error: {e}")        # Error: unhashable type: 'list'
```

### Output

```
<class 'dict'>
<class 'dict'>
{'name': 'Alex', 'age': 25, 'city': 'Hyderabad'}
{'name': 'Bob', 'age': 30, 'city': 'Delhi'}
{'a': 1, 'b': 2, 'c': 3}
{'name': 'Alice', 'age': 22, 'score': 95.5}
{1: 'one', 'two': 2, (3, 4): 'tuple_key', 'list_val': [1, 2, 3]}
{'a': 99, 'b': 2}
{'student': {'name': 'Alex', 'grade': 'A'}, 'scores': {'math': 95, 'science': 88}}
{'a': 0, 'b': 0, 'c': 0, 'd': 0}
{'x': None, 'y': None, 'z': None}
Error: unhashable type: 'list'
```

---

## 3. Accessing Values

```python
student = {"name": "Alex", "age": 25, "city": "Hyderabad", "score": 92.5}

# Method 1: Square bracket notation — raises KeyError if key absent
print(student["name"])          # Alex
print(student["score"])         # 92.5

# KeyError when key doesn't exist
try:
    print(student["grade"])
except KeyError as e:
    print(f"KeyError: {e}")     # KeyError: 'grade'

# Method 2: get() — safe access, returns None or default if key absent
print(student.get("name"))      # Alex
print(student.get("grade"))     # None  (no error)
print(student.get("grade", "N/A"))  # N/A  (custom default)

# Nested dictionary access
data = {
    "employee": {
        "name": "Alice",
        "address": {
            "city": "Mumbai",
            "pin": 400001
        }
    }
}
print(data["employee"]["name"])                     # Alice
print(data["employee"]["address"]["city"])          # Mumbai
print(data.get("employee", {}).get("address", {}).get("pin"))  # 400001 (safe chain)

# Accessing all keys, values, items
print(student.keys())           # dict_keys(['name', 'age', 'city', 'score'])
print(student.values())         # dict_values(['Alex', 25, 'Hyderabad', 92.5])
print(student.items())          # dict_items([('name', 'Alex'), ...])

# Check before access (preferred over try/except for simple cases)
key = "age"
if key in student:
    print(student[key])         # 25
```

### Output

```
Alex
92.5
KeyError: 'grade'
Alex
None
N/A
Alice
Mumbai
400001
dict_keys(['name', 'age', 'city', 'score'])
dict_values(['Alex', 25, 'Hyderabad', 92.5])
dict_items([('name', 'Alex'), ('age', 25), ('city', 'Hyderabad'), ('score', 92.5)])
25
```

---

## 4. Adding & Updating Elements

```python
d = {"name": "Alex", "age": 25}

# Add new key-value pair
d["city"] = "Hyderabad"
print(d)        # {'name': 'Alex', 'age': 25, 'city': 'Hyderabad'}

# Update existing key
d["age"] = 26
print(d)        # {'name': 'Alex', 'age': 26, 'city': 'Hyderabad'}

# update() — add/update multiple keys at once
d.update({"score": 95, "grade": "A"})
print(d)

# update() with keyword arguments
d.update(city="Chennai", age=27)
print(d)

# update() with iterable of pairs
d.update([("email", "alex@email.com"), ("phone", "9999999999")])
print(d)

# setdefault() — set key only if it DOESN'T exist
d.setdefault("country", "India")    # "country" not in d → adds it
print(d.get("country"))             # India

d.setdefault("age", 99)             # "age" already exists → does NOT overwrite
print(d.get("age"))                 # 27  (unchanged)

# Merging two dicts — Python 3.9+ operator |
d1 = {"a": 1, "b": 2}
d2 = {"b": 99, "c": 3}
merged = d1 | d2            # d2 values win on conflict
print(merged)               # {'a': 1, 'b': 99, 'c': 3}

d1 |= d2                    # In-place merge
print(d1)                   # {'a': 1, 'b': 99, 'c': 3}

# Pre-3.9 merge using unpacking
d3 = {"x": 10}
d4 = {"y": 20}
merged2 = {**d3, **d4}
print(merged2)              # {'x': 10, 'y': 20}
```

### Output

```
{'name': 'Alex', 'age': 25, 'city': 'Hyderabad'}
{'name': 'Alex', 'age': 26, 'city': 'Hyderabad'}
{'name': 'Alex', 'age': 26, 'city': 'Hyderabad', 'score': 95, 'grade': 'A'}
{'name': 'Alex', 'age': 27, 'city': 'Chennai', 'score': 95, 'grade': 'A'}
{'name': 'Alex', 'age': 27, 'city': 'Chennai', 'score': 95, 'grade': 'A', 'email': 'alex@email.com', 'phone': '9999999999'}
India
27
{'a': 1, 'b': 99, 'c': 3}
{'a': 1, 'b': 99, 'c': 3}
{'x': 10, 'y': 20}
```

---

## 5. Deleting Elements

```python
d = {"name": "Alex", "age": 25, "city": "Hyderabad", "score": 92, "grade": "A"}

# del — removes key; raises KeyError if not found
del d["grade"]
print(d)

try:
    del d["salary"]
except KeyError as e:
    print(f"KeyError: {e}")     # KeyError: 'salary'

# pop(key) — removes and RETURNS the value; optional default
age = d.pop("age")
print(f"Removed age: {age}")    # Removed age: 25
print(d)

# pop with default — no error if key absent
salary = d.pop("salary", 0)
print(f"Salary (default): {salary}")   # Salary (default): 0

# popitem() — removes and returns the LAST inserted (key, value) pair
last = d.popitem()
print(f"Popped last item: {last}")     # Popped last item: ('score', 92)
print(d)

# clear() — removes ALL items, dict remains
d.clear()
print(d)                        # {}
print(type(d))                  # <class 'dict'>

# del the entire dictionary variable
d2 = {"a": 1}
del d2
try:
    print(d2)
except NameError as e:
    print(f"NameError: {e}")    # NameError: name 'd2' is not defined
```

### Output

```
{'name': 'Alex', 'age': 25, 'city': 'Hyderabad', 'score': 92}
KeyError: 'salary'
Removed age: 25
{'name': 'Alex', 'city': 'Hyderabad', 'score': 92}
Salary (default): 0
Popped last item: ('score', 92)
{'name': 'Alex', 'city': 'Hyderabad'}
{}
<class 'dict'>
NameError: name 'd2' is not defined
```

---

## 6. Mathematical Operators

Dictionaries support a limited set of operators. Most arithmetic (`+`, `-`, `*`, `/`) do NOT apply to whole dicts.

```python
d1 = {"a": 1, "b": 2}
d2 = {"b": 99, "c": 3}

# | Merge (Python 3.9+) — creates new dict; right side wins on conflict
merged = d1 | d2
print(merged)               # {'a': 1, 'b': 99, 'c': 3}

# |= Merge in-place (Python 3.9+)
d1 |= d2
print(d1)                   # {'a': 1, 'b': 99, 'c': 3}

# ** Unpacking merge (all Python versions)
d3 = {"x": 10, "y": 20}
d4 = {"y": 99, "z": 30}
result = {**d3, **d4}       # Right dict wins on conflict
print(result)               # {'x': 10, 'y': 99, 'z': 30}

# Arithmetic on VALUES (not the dict itself)
prices = {"apple": 50, "banana": 30, "cherry": 80}

# Apply 10% discount
discounted = {k: round(v * 0.9, 2) for k, v in prices.items()}
print(discounted)           # {'apple': 45.0, 'banana': 27.0, 'cherry': 72.0}

# Sum all values
print(sum(prices.values())) # 160

# Multiply all values by 2
doubled = {k: v * 2 for k, v in prices.items()}
print(doubled)              # {'apple': 100, 'banana': 60, 'cherry': 160}

# What does NOT work
try:
    print(d3 + d4)
except TypeError as e:
    print(f"Error: {e}")    # Error: unsupported operand type(s) for +: 'dict' and 'dict'
```

### Output

```
{'a': 1, 'b': 99, 'c': 3}
{'a': 1, 'b': 99, 'c': 3}
{'x': 10, 'y': 99, 'z': 30}
{'apple': 45.0, 'banana': 27.0, 'cherry': 72.0}
160
{'apple': 100, 'banana': 60, 'cherry': 160}
Error: unsupported operand type(s) for +: 'dict' and 'dict'
```

---

## 7. Membership Operators

`in` and `not in` check **keys only** by default — not values.

```python
student = {"name": "Alex", "age": 25, "city": "Hyderabad"}

# in — checks KEYS only
print("name" in student)        # True
print("Alex" in student)        # False  — "Alex" is a value, not a key
print("salary" in student)      # False

# not in
print("salary" not in student)  # True
print("age" not in student)     # False

# Check if a VALUE exists
print("Alex" in student.values())       # True
print("Mumbai" in student.values())     # False

# Check if a key-value PAIR exists
print(("name", "Alex") in student.items())     # True
print(("name", "Bob")  in student.items())     # False

# Practical — safe access pattern
key = "score"
if key in student:
    print(student[key])
else:
    print(f"'{key}' not found in student record")

# Nested dict membership
data = {"scores": {"math": 90, "science": 85}}
print("scores" in data)                 # True
print("math" in data.get("scores", {})) # True
```

### Output

```
True
False
False
True
False
True
False
True
False
'score' not found in student record
True
True
```

---

## 8. Comparison Operators

Dictionaries support `==` and `!=`. They compare all key-value pairs regardless of insertion order.

```python
d1 = {"a": 1, "b": 2, "c": 3}
d2 = {"b": 2, "a": 1, "c": 3}   # Same pairs, different insertion order
d3 = {"a": 1, "b": 2, "c": 99}  # Different value for "c"
d4 = {"a": 1, "b": 2}           # Missing "c"

# Equality — order doesn't matter, content does
print(d1 == d2)     # True  — same key-value pairs
print(d1 == d3)     # False — "c" has different value
print(d1 == d4)     # False — different number of keys

# Inequality
print(d1 != d3)     # True
print(d1 != d2)     # False

# < > <= >= are NOT supported for dicts
try:
    print(d1 < d3)
except TypeError as e:
    print(f"Error: {e}")   # Error: '<' not supported between 'dict' and 'dict'

# Comparing specific values
scores1 = {"Alice": 85, "Bob": 92}
scores2 = {"Alice": 85, "Bob": 92}
scores3 = {"Alice": 85, "Bob": 78}

print(scores1 == scores2)   # True
print(scores1 == scores3)   # False

# Practical comparison — check if config changed
old_config = {"debug": False, "host": "localhost", "port": 8080}
new_config = {"debug": True,  "host": "localhost", "port": 8080}

if old_config != new_config:
    changed = {k for k in old_config if old_config.get(k) != new_config.get(k)}
    print(f"Changed settings: {changed}")   # Changed settings: {'debug'}
```

### Output

```
True
False
False
True
False
Error: '<' not supported between instances of 'dict' and 'dict'
True
False
Changed settings: {'debug'}
```

---

## 9. Built-in Functions

```python
inventory = {"apples": 50, "bananas": 30, "cherries": 80, "dates": 20}

# len() — number of key-value pairs
print(len(inventory))           # 4

# max() and min() — on keys by default
print(max(inventory))           # dates     (lexicographic max key)
print(min(inventory))           # apples    (lexicographic min key)

# max/min on values
print(max(inventory.values()))  # 80
print(min(inventory.values()))  # 20

# max/min on keys sorted by value
print(max(inventory, key=inventory.get))    # cherries  (key with max value)
print(min(inventory, key=inventory.get))    # dates     (key with min value)

# sum() — on values
print(sum(inventory.values()))  # 180

# sorted() — on keys
print(sorted(inventory))                        # ['apples', 'bananas', 'cherries', 'dates']
print(sorted(inventory, reverse=True))          # ['dates', 'cherries', 'bananas', 'apples']

# sorted by value
print(sorted(inventory, key=lambda k: inventory[k]))            # ascending by value
print(sorted(inventory, key=lambda k: inventory[k], reverse=True))  # descending by value

# any() and all() — on keys
d = {"a": 0, "b": 1, "c": 2}
print(any(d))               # True   — keys are truthy strings
print(all(d))               # True   — all keys are truthy

# any/all on values
print(any(d.values()))      # True   — 1 and 2 are truthy
print(all(d.values()))      # False  — 0 is falsy

# enumerate() on keys
for i, key in enumerate(sorted(inventory)):
    print(f"  {i+1}. {key}: {inventory[key]}")

# type()
print(type(inventory))      # <class 'dict'>

# list(), tuple() — convert keys
print(list(inventory))          # ['apples', 'bananas', 'cherries', 'dates']
print(tuple(inventory))         # ('apples', 'bananas', 'cherries', 'dates')
```

### Output

```
4
dates
apples
80
20
cherries
dates
180
['apples', 'bananas', 'cherries', 'dates']
['dates', 'cherries', 'bananas', 'apples']
['dates', 'apples', 'bananas', 'cherries']
['cherries', 'bananas', 'apples', 'dates']
True
True
True
False
  1. apples: 50
  2. bananas: 30
  3. cherries: 80
  4. dates: 20
<class 'dict'>
['apples', 'bananas', 'cherries', 'dates']
('apples', 'bananas', 'cherries', 'dates')
```

---

## 10. Iteration — keys, values, items

```python
student = {"name": "Alex", "age": 25, "city": "Hyderabad", "score": 92}

# Iterate over KEYS (default)
print("Keys:")
for key in student:
    print(f"  {key}")

# Iterate over KEYS explicitly
print("Keys via .keys():")
for key in student.keys():
    print(f"  {key}")

# Iterate over VALUES
print("Values:")
for value in student.values():
    print(f"  {value}")

# Iterate over KEY-VALUE PAIRS (most common)
print("Items:")
for key, value in student.items():
    print(f"  {key}: {value}")

# Iterate with enumerate
print("Enumerated items:")
for i, (key, value) in enumerate(student.items(), start=1):
    print(f"  {i}. {key} → {value}")

# Sorted iteration
print("Sorted by key:")
for key in sorted(student):
    print(f"  {key}: {student[key]}")

print("Sorted by value (numeric only):")
scores = {"Alice": 85, "Bob": 92, "Charlie": 78, "David": 95}
for name, score in sorted(scores.items(), key=lambda x: x[1], reverse=True):
    print(f"  {name}: {score}")

# Conditional iteration
print("Keys with value > 50:")
inventory = {"apples": 50, "bananas": 30, "cherries": 80, "dates": 20}
for k, v in inventory.items():
    if v > 40:
        print(f"  {k}: {v}")

# Nested dict iteration
employees = {
    "E001": {"name": "Alice", "dept": "Engineering"},
    "E002": {"name": "Bob",   "dept": "Marketing"},
}
for emp_id, details in employees.items():
    print(f"  {emp_id}: {details['name']} — {details['dept']}")
```

### Output

```
Keys:
  name
  age
  city
  score
Keys via .keys():
  name  age  city  score
Values:
  Alex  25  Hyderabad  92
Items:
  name: Alex
  age: 25
  city: Hyderabad
  score: 92
Enumerated items:
  1. name → Alex
  2. age → 25
  3. city → Hyderabad
  4. score → 92
Sorted by key:
  age: 25
  city: Hyderabad
  name: Alex
  score: 92
Sorted by value (numeric only):
  David: 95
  Bob: 92
  Alice: 85
  Charlie: 78
Keys with value > 50:
  apples: 50
  cherries: 80
E001: Alice — Engineering
E002: Bob — Marketing
```

---

## 11. Dictionary Methods

Here is a complete reference of all built-in dictionary methods.

```python
d = {"name": "Alex", "age": 25, "city": "Hyderabad"}

# ── READ METHODS ──────────────────────────────────────────────

# keys() — returns dict_keys view
print(d.keys())             # dict_keys(['name', 'age', 'city'])

# values() — returns dict_values view
print(d.values())           # dict_values(['Alex', 25, 'Hyderabad'])

# items() — returns dict_items view of (key, value) tuples
print(d.items())            # dict_items([('name', 'Alex'), ('age', 25), ('city', 'Hyderabad')])

# get(key, default) — safe value access
print(d.get("name"))        # Alex
print(d.get("salary"))      # None
print(d.get("salary", 0))   # 0

# ── WRITE METHODS ─────────────────────────────────────────────

# update() — add/overwrite multiple keys
d.update({"score": 95, "grade": "A"})
print(d)

# setdefault(key, default) — insert key only if absent; returns value
val = d.setdefault("country", "India")
print(val)                  # India   (added)
val2 = d.setdefault("age", 99)
print(val2)                 # 25      (not changed — key existed)

# ── DELETE METHODS ────────────────────────────────────────────

# pop(key, default) — remove and return value
removed = d.pop("grade", "N/A")
print(removed)              # A

# popitem() — remove and return last (key, value) pair
last = d.popitem()
print(last)                 # ('country', 'India')

# clear() — empty the dict
d2 = {"a": 1, "b": 2}
d2.clear()
print(d2)                   # {}

# ── COPY METHODS ──────────────────────────────────────────────

original = {"a": [1, 2, 3], "b": 99}

# copy() — shallow copy
shallow = original.copy()
shallow["b"] = 0             # Does NOT affect original
shallow["a"].append(4)       # DOES affect original (shared list reference)
print(original)             # {'a': [1, 2, 3, 4], 'b': 99}
print(shallow)              # {'a': [1, 2, 3, 4], 'b': 0}

# Deep copy — use copy module
import copy
deep = copy.deepcopy(original)
deep["a"].append(99)
print(original["a"])        # [1, 2, 3, 4]   — unchanged
print(deep["a"])            # [1, 2, 3, 4, 99]

# ── CLASS METHOD ─────────────────────────────────────────────

# fromkeys(iterable, value) — class method
d3 = dict.fromkeys(["a", "b", "c"], 0)
print(d3)                   # {'a': 0, 'b': 0, 'c': 0}

# Gotcha: mutable default is SHARED
d4 = dict.fromkeys(["x", "y"], [])
d4["x"].append(1)
print(d4)                   # {'x': [1], 'y': [1]}  ← both affected!

# Fix: use comprehension instead
d5 = {k: [] for k in ["x", "y"]}
d5["x"].append(1)
print(d5)                   # {'x': [1], 'y': []}  ← independent lists ✅
```

### Complete Methods Quick Reference

| Method | Description | Returns |
|--------|-------------|---------|
| `keys()` | All keys | `dict_keys` view |
| `values()` | All values | `dict_values` view |
| `items()` | All key-value pairs | `dict_items` view |
| `get(k, d)` | Value for key, or default | value or `None` |
| `update(other)` | Merge another dict/iterable | `None` |
| `setdefault(k, d)` | Insert key if absent | existing or new value |
| `pop(k, d)` | Remove key, return value | value |
| `popitem()` | Remove & return last pair | `(key, value)` tuple |
| `clear()` | Remove all items | `None` |
| `copy()` | Shallow copy | new `dict` |
| `fromkeys(it, v)` | New dict from keys | new `dict` |

---

## 12. Dictionary Comprehension

Dictionary comprehension provides a concise way to create dictionaries from iterables.

**Syntax:** `{key_expr: value_expr for item in iterable if condition}`

```python
# Basic comprehension
squares = {x: x**2 for x in range(1, 6)}
print(squares)          # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# With condition — only even numbers
even_squares = {x: x**2 for x in range(1, 11) if x % 2 == 0}
print(even_squares)     # {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}

# Reverse a dictionary (swap keys and values)
original = {"a": 1, "b": 2, "c": 3}
reversed_d = {v: k for k, v in original.items()}
print(reversed_d)       # {1: 'a', 2: 'b', 3: 'c'}

# Filter dict — keep only items where value > threshold
scores = {"Alice": 85, "Bob": 60, "Charlie": 92, "David": 55, "Eve": 78}
passed = {name: score for name, score in scores.items() if score >= 70}
print(passed)           # {'Alice': 85, 'Charlie': 92, 'Eve': 78}

# Transform values — uppercase all string values
info = {"name": "alex", "city": "hyderabad", "country": "india"}
upper_info = {k: v.upper() for k, v in info.items()}
print(upper_info)       # {'name': 'ALEX', 'city': 'HYDERABAD', 'country': 'INDIA'}

# From two lists
names  = ["Alice", "Bob", "Charlie"]
scores_list = [85, 92, 78]
score_map = {name: score for name, score in zip(names, scores_list)}
print(score_map)        # {'Alice': 85, 'Bob': 92, 'Charlie': 78}

# Word frequency counter
sentence = "the cat sat on the mat the cat"
freq = {word: sentence.split().count(word) for word in set(sentence.split())}
print(freq)             # {'the': 3, 'cat': 2, 'sat': 1, 'on': 1, 'mat': 1}

# Nested dict comprehension
matrix = {i: {j: i * j for j in range(1, 4)} for i in range(1, 4)}
for row, cols in matrix.items():
    print(f"  {row}: {cols}")
# 1: {1: 1, 2: 2, 3: 3}
# 2: {1: 2, 2: 4, 3: 6}
# 3: {1: 3, 2: 6, 3: 9}

# Conditional value transformation
grades = {"Alice": 85, "Bob": 60, "Charlie": 92, "David": 55}
grade_letters = {
    name: "Pass" if score >= 60 else "Fail"
    for name, score in grades.items()
}
print(grade_letters)    # {'Alice': 'Pass', 'Bob': 'Pass', 'Charlie': 'Pass', 'David': 'Fail'}
```

### Output

```
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
{2: 4, 4: 16, 6: 36, 8: 64, 10: 100}
{1: 'a', 2: 'b', 3: 'c'}
{'Alice': 85, 'Charlie': 92, 'Eve': 78}
{'name': 'ALEX', 'city': 'HYDERABAD', 'country': 'INDIA'}
{'Alice': 85, 'Bob': 92, 'Charlie': 78}
{'the': 3, 'cat': 2, 'sat': 1, 'on': 1, 'mat': 1}
  1: {1: 1, 2: 2, 3: 3}
  2: {1: 2, 2: 4, 3: 6}
  3: {1: 3, 2: 6, 3: 9}
{'Alice': 'Pass', 'Bob': 'Pass', 'Charlie': 'Pass', 'David': 'Fail'}
```

---

## 13. Nested Dictionaries

A nested dictionary is a dictionary where values are themselves dictionaries.

```python
# Creating nested dict
company = {
    "E001": {
        "name": "Alice",
        "age": 30,
        "dept": "Engineering",
        "skills": ["Python", "SQL", "ML"],
        "salary": 85000
    },
    "E002": {
        "name": "Bob",
        "age": 28,
        "dept": "Marketing",
        "skills": ["SEO", "Content", "Analytics"],
        "salary": 65000
    },
    "E003": {
        "name": "Charlie",
        "age": 35,
        "dept": "Engineering",
        "skills": ["Java", "Docker", "AWS"],
        "salary": 95000
    }
}

# Accessing nested values
print(company["E001"]["name"])              # Alice
print(company["E002"]["skills"][1])         # Content
print(company["E003"]["salary"])            # 95000

# Safe nested access
print(company.get("E004", {}).get("name", "Not found"))   # Not found

# Adding to nested dict
company["E001"]["projects"] = ["AI Dashboard", "CRM Tool"]
print(company["E001"]["projects"])

# Updating nested value
company["E002"]["salary"] = 70000

# Iterating nested dict
print("\nEmployee Report:")
for emp_id, details in company.items():
    print(f"\n  ID: {emp_id}")
    for key, value in details.items():
        print(f"    {key}: {value}")

# Filtering from nested dict
engineering = {
    emp_id: details
    for emp_id, details in company.items()
    if details["dept"] == "Engineering"
}
print("\nEngineering team:", list(engineering.keys()))

# Find highest paid employee
top_earner = max(company, key=lambda e: company[e]["salary"])
print(f"Top earner: {company[top_earner]['name']} — ₹{company[top_earner]['salary']}")

# Aggregate: total salary by department
dept_salaries = {}
for emp in company.values():
    dept = emp["dept"]
    dept_salaries[dept] = dept_salaries.get(dept, 0) + emp["salary"]
print("Dept salaries:", dept_salaries)
```

### Output

```
Alice
Content
95000
Not found
['AI Dashboard', 'CRM Tool']

Employee Report:
  ID: E001
    name: Alice
    age: 30
    ...

Engineering team: ['E001', 'E003']
Top earner: Charlie — ₹95000
Dept salaries: {'Engineering': 180000, 'Marketing': 70000}
```

---

## 14. Dictionary vs List vs Set vs Tuple

| Feature | Dictionary | List | Set | Tuple |
|---------|-----------|------|-----|-------|
| **Syntax** | `{k:v}` | `[1,2]` | `{1,2}` | `(1,2)` |
| **Ordered** | ✅ (3.7+) | ✅ | ❌ | ✅ |
| **Mutable** | ✅ | ✅ | ✅ | ❌ |
| **Duplicates** | ❌ Keys unique | ✅ | ❌ | ✅ |
| **Indexed** | By key | By int | ❌ | By int |
| **Lookup** | O(1) by key | O(n) | O(1) | O(n) |
| **Hashable** | ❌ | ❌ | ❌ | ✅ |
| **Use case** | Key-value mapping | Ordered sequence | Unique items | Fixed data |

```python
import sys

d = {"a": 1, "b": 2, "c": 3}
l = [1, 2, 3]
s = {1, 2, 3}
t = (1, 2, 3)

print(f"dict  size: {sys.getsizeof(d)} bytes")   # ~232 bytes
print(f"list  size: {sys.getsizeof(l)} bytes")   # ~120 bytes
print(f"set   size: {sys.getsizeof(s)} bytes")   # ~216 bytes
print(f"tuple size: {sys.getsizeof(t)} bytes")   # ~80 bytes

# Choose the right structure:
# dict  → student record, config, word frequency, JSON-like data
# list  → ordered queue, log entries, items to process
# set   → unique emails, visited URLs, tags
# tuple → coordinates, RGB, DB row, function return values
```

---

## 15. 15 Interview Programs

---

### Program 1: Word Frequency Counter

```python
def word_frequency(text):
    words = text.lower().split()
    freq = {}
    for word in words:
        freq[word] = freq.get(word, 0) + 1
    return freq

text = "the quick brown fox jumps over the lazy dog the fox"
freq = word_frequency(text)

# Sort by frequency descending
for word, count in sorted(freq.items(), key=lambda x: x[1], reverse=True):
    print(f"  {word}: {count}")
```

**Output:**
```
  the: 3
  fox: 2
  quick: 1
  brown: 1
  jumps: 1
  over: 1
  lazy: 1
  dog: 1
```

---

### Program 2: Reverse a Dictionary (Swap Keys and Values)

```python
def reverse_dict(d):
    return {v: k for k, v in d.items()}

original = {"a": 1, "b": 2, "c": 3}
print(reverse_dict(original))    # {1: 'a', 2: 'b', 3: 'c'}

# Handle duplicate values
def reverse_dict_safe(d):
    """Group keys that share the same value"""
    result = {}
    for k, v in d.items():
        result.setdefault(v, []).append(k)
    return result

d2 = {"a": 1, "b": 2, "c": 1, "d": 3, "e": 2}
print(reverse_dict_safe(d2))    # {1: ['a', 'c'], 2: ['b', 'e'], 3: ['d']}
```

**Output:**
```
{1: 'a', 2: 'b', 3: 'c'}
{1: ['a', 'c'], 2: ['b', 'e'], 3: ['d']}
```

---

### Program 3: Find the Key with Maximum Value

```python
def key_with_max_value(d):
    return max(d, key=d.get)

def key_with_min_value(d):
    return min(d, key=d.get)

scores = {"Alice": 85, "Bob": 92, "Charlie": 78, "David": 95, "Eve": 88}
print(f"Highest scorer: {key_with_max_value(scores)}")   # David
print(f"Lowest scorer:  {key_with_min_value(scores)}")   # Charlie
```

**Output:**
```
Highest scorer: David
Lowest scorer:  Charlie
```

---

### Program 4: Merge Two Dictionaries and Sum Common Keys

```python
def merge_and_sum(d1, d2):
    merged = d1.copy()
    for k, v in d2.items():
        merged[k] = merged.get(k, 0) + v
    return merged

sales_jan = {"apples": 50, "bananas": 30, "cherries": 20}
sales_feb = {"bananas": 45, "cherries": 35, "dates": 60}

total = merge_and_sum(sales_jan, sales_feb)
print(total)
# {'apples': 50, 'bananas': 75, 'cherries': 55, 'dates': 60}
```

**Output:**
```
{'apples': 50, 'bananas': 75, 'cherries': 55, 'dates': 60}
```

---

### Program 5: Group Elements by a Property

```python
def group_by(lst, key_func):
    groups = {}
    for item in lst:
        key = key_func(item)
        groups.setdefault(key, []).append(item)
    return groups

# Group by first letter
words = ["apple", "banana", "avocado", "blueberry", "cherry", "apricot", "cranberry"]
grouped = group_by(words, lambda w: w[0].upper())
for letter, ws in sorted(grouped.items()):
    print(f"  {letter}: {ws}")
```

**Output:**
```
  A: ['apple', 'avocado', 'apricot']
  B: ['banana', 'blueberry']
  C: ['cherry', 'cranberry']
```

---

### Program 6: Check if Two Strings are Anagrams Using Dict

```python
def are_anagrams(s1, s2):
    def char_freq(s):
        freq = {}
        for ch in s.lower().replace(" ", ""):
            freq[ch] = freq.get(ch, 0) + 1
        return freq
    return char_freq(s1) == char_freq(s2)

print(are_anagrams("listen", "silent"))     # True
print(are_anagrams("hello", "world"))       # False
print(are_anagrams("Astronomer", "Moon starer"))  # True
```

**Output:**
```
True
False
True
```

---

### Program 7: Find All Duplicate Values in a Dictionary

```python
def find_duplicate_values(d):
    seen = {}
    duplicates = {}
    for k, v in d.items():
        if v in seen:
            duplicates.setdefault(v, [seen[v]]).append(k)
        else:
            seen[v] = k
    return duplicates

d = {"a": 1, "b": 2, "c": 1, "d": 3, "e": 2, "f": 1}
dups = find_duplicate_values(d)
for val, keys in dups.items():
    print(f"  Value {val} → keys: {keys}")
```

**Output:**
```
  Value 1 → keys: ['a', 'c', 'f']
  Value 2 → keys: ['b', 'e']
```

---

### Program 8: Sort Dictionary by Value

```python
scores = {"Alice": 85, "Bob": 92, "Charlie": 78, "David": 95, "Eve": 88}

# Sort ascending by value
asc = dict(sorted(scores.items(), key=lambda x: x[1]))
print("Ascending:", asc)

# Sort descending by value
desc = dict(sorted(scores.items(), key=lambda x: x[1], reverse=True))
print("Descending:", desc)

# Top 3 scorers
top3 = dict(list(desc.items())[:3])
print("Top 3:", top3)
```

**Output:**
```
Ascending: {'Charlie': 78, 'Alice': 85, 'Eve': 88, 'Bob': 92, 'David': 95}
Descending: {'David': 95, 'Bob': 92, 'Eve': 88, 'Alice': 85, 'Charlie': 78}
Top 3: {'David': 95, 'Bob': 92, 'Eve': 88}
```

---

### Program 9: Flatten a Nested Dictionary

```python
def flatten_dict(d, parent_key="", sep="."):
    items = {}
    for k, v in d.items():
        new_key = f"{parent_key}{sep}{k}" if parent_key else k
        if isinstance(v, dict):
            items.update(flatten_dict(v, new_key, sep))
        else:
            items[new_key] = v
    return items

nested = {
    "person": {
        "name": "Alex",
        "address": {
            "city": "Hyderabad",
            "pin": 500001
        }
    },
    "score": 95
}

flat = flatten_dict(nested)
for k, v in flat.items():
    print(f"  {k}: {v}")
```

**Output:**
```
  person.name: Alex
  person.address.city: Hyderabad
  person.address.pin: 500001
  score: 95
```

---

### Program 10: Count Character Frequency in a String

```python
def char_frequency(s):
    freq = {}
    for ch in s:
        if ch != ' ':
            freq[ch] = freq.get(ch, 0) + 1
    return dict(sorted(freq.items(), key=lambda x: x[1], reverse=True))

text = "programming"
freq = char_frequency(text)
for char, count in freq.items():
    bar = "█" * count
    print(f"  '{char}': {bar} ({count})")
```

**Output:**
```
  'g': ██ (2)
  'r': ██ (2)
  'm': ██ (2)
  'p': █ (1)
  'o': █ (1)
  'a': █ (1)
  'i': █ (1)
  'n': █ (1)
```

---

### Program 11: Find Common Keys Between Two Dictionaries

```python
def common_keys(d1, d2):
    return set(d1.keys()) & set(d2.keys())

def common_key_same_value(d1, d2):
    common = common_keys(d1, d2)
    return {k for k in common if d1[k] == d2[k]}

d1 = {"a": 1, "b": 2, "c": 3, "d": 4}
d2 = {"b": 2, "c": 99, "d": 4, "e": 5}

print("Common keys:", common_keys(d1, d2))                  # {'b', 'c', 'd'}
print("Same value:", common_key_same_value(d1, d2))          # {'b', 'd'}
print("Different value:", common_keys(d1,d2) - common_key_same_value(d1,d2))  # {'c'}
```

**Output:**
```
Common keys: {'b', 'c', 'd'}
Same value: {'b', 'd'}
Different value: {'c'}
```

---

### Program 12: Implement a Simple Phone Book

```python
class PhoneBook:
    def __init__(self):
        self.book = {}

    def add(self, name, number):
        self.book[name] = number
        print(f"Added: {name} → {number}")

    def lookup(self, name):
        return self.book.get(name, "Contact not found")

    def delete(self, name):
        if name in self.book:
            del self.book[name]
            print(f"Deleted: {name}")
        else:
            print(f"{name} not found")

    def display(self):
        print("\nPhone Book:")
        for name, num in sorted(self.book.items()):
            print(f"  {name}: {num}")

pb = PhoneBook()
pb.add("Alice", "9876543210")
pb.add("Bob",   "8765432109")
pb.add("Charlie","7654321098")
print(pb.lookup("Alice"))       # 9876543210
print(pb.lookup("David"))       # Contact not found
pb.delete("Bob")
pb.display()
```

**Output:**
```
Added: Alice → 9876543210
Added: Bob → 8765432109
Added: Charlie → 7654321098
9876543210
Contact not found
Deleted: Bob

Phone Book:
  Alice: 9876543210
  Charlie: 7654321098
```

---

### Program 13: Find the First Non-Repeating Character

```python
def first_non_repeating(s):
    freq = {}
    for ch in s:
        freq[ch] = freq.get(ch, 0) + 1

    for ch in s:            # preserve original order
        if freq[ch] == 1:
            return ch
    return None

print(first_non_repeating("swiss"))         # w
print(first_non_repeating("aabbcc"))        # None
print(first_non_repeating("programming"))   # p
```

**Output:**
```
w
None
p
```

---

### Program 14: Group Anagrams Together

```python
def group_anagrams(words):
    groups = {}
    for word in words:
        key = tuple(sorted(word))       # Canonical form
        groups.setdefault(key, []).append(word)
    return list(groups.values())

words = ["eat", "tea", "tan", "ate", "nat", "bat", "listen", "silent", "enlist"]
groups = group_anagrams(words)
for group in groups:
    print(f"  {group}")
```

**Output:**
```
  ['eat', 'tea', 'ate']
  ['tan', 'nat']
  ['bat']
  ['listen', 'silent', 'enlist']
```

---

### Program 15: Student Grade Report Using Nested Dict

```python
def generate_report(students):
    print(f"{'Name':<12} {'Math':>6} {'Sci':>6} {'Eng':>6} {'Avg':>7} {'Grade':>6}")
    print("-" * 48)
    for name, marks in sorted(students.items()):
        avg = sum(marks.values()) / len(marks)
        grade = "A" if avg >= 85 else "B" if avg >= 70 else "C" if avg >= 55 else "F"
        print(f"{name:<12} {marks['Math']:>6} {marks['Science']:>6} {marks['English']:>6} {avg:>7.1f} {grade:>6}")

students = {
    "Alice":   {"Math": 92, "Science": 88, "English": 95},
    "Bob":     {"Math": 65, "Science": 72, "English": 68},
    "Charlie": {"Math": 78, "Science": 82, "English": 74},
    "David":   {"Math": 45, "Science": 52, "English": 60},
    "Eve":     {"Math": 88, "Science": 91, "English": 87},
}

generate_report(students)
```

**Output:**
```
Name           Math   Sci   Eng     Avg  Grade
------------------------------------------------
Alice            92    88    95    91.7      A
Bob              65    72    68    68.3      C
Charlie          78    82    74    78.0      B
David            45    52    60    52.3      F
Eve              88    91    87    88.7      A
```

---

## 16. Summary

| Topic | Key Points |
|-------|-----------|
| **Definition** | Ordered, mutable key-value collection |
| **Creation** | `{}`, `dict()`, `dict(zip(...))`, `dict.fromkeys()`, comprehension |
| **Empty dict** | `{}` or `dict()` — note `{}` is dict, NOT set |
| **Access** | `d[key]` (KeyError if absent), `d.get(key, default)` (safe) |
| **Add/Update** | `d[key] = val`, `update()`, `setdefault()`, `\|=` (3.9+) |
| **Delete** | `del d[key]`, `pop(k, default)`, `popitem()`, `clear()` |
| **Operators** | `\|` merge (3.9+), `**` unpack-merge, no `+`/`-`/`*` on dicts |
| **Membership** | `in`/`not in` checks **keys only** by default |
| **Comparison** | `==` and `!=` only; no `<`, `>` |
| **Built-ins** | `len`, `max`, `min`, `sum`, `sorted`, `any`, `all` |
| **Iteration** | `.keys()`, `.values()`, `.items()` — all return view objects |
| **Methods** | `get`, `update`, `setdefault`, `pop`, `popitem`, `clear`, `copy`, `fromkeys` |
| **Comprehension** | `{k: v for k, v in ...}` — powerful one-liner dicts |
| **Nested** | Dict of dicts for structured data; use `.get()` chains safely |
| **vs others** | Dict wins for key-value lookup; set wins for membership; list for ordering |

### Golden Rules

```python
# 1. Use get() instead of [] when key may be absent
value = d.get("key", "default")   # ✅ safe

# 2. Use setdefault() to initialize lists/counts without overwriting
d.setdefault("scores", []).append(95)   # ✅

# 3. in checks keys only — use .values() or .items() for the rest
"Alex" in d               # checks keys
"Alex" in d.values()      # checks values ✅

# 4. Keys must be hashable — strings, ints, tuples work; lists don't
d = {(1, 2): "point"}     # ✅ tuple key
# d = {[1, 2]: "point"}   # ❌ TypeError

# 5. dict.fromkeys() with mutable default is a trap
d = dict.fromkeys(["a","b"], [])   # ❌ SHARED list
d = {k: [] for k in ["a","b"]}    # ✅ INDEPENDENT lists
```

---

## 17. Self-Study Exercises

### Level 1 — Basic

1. Create a dictionary of 5 countries and their capitals. Print the capital of any three countries using `[]` and `get()`.
2. Write a program to add a new key `"population"` to an existing country dictionary and update the capital of one country.
3. Given `d = {"a": 10, "b": 20, "c": 30}`, delete key `"b"` using `del` and `"c"` using `pop()`. Print the result.
4. Write a program to check if a key `"score"` exists in a student dictionary before accessing it.
5. Use `dict.fromkeys()` to create a dictionary with keys `["Mon", "Tue", "Wed", "Thu", "Fri"]` and default value `0` (attendance counter).

### Level 2 — Intermediate

6. Write a program to count the frequency of each character in a given string using a dictionary (without using `Counter`).
7. Given a list of tuples `[("Alice", 85), ("Bob", 92), ("Alice", 78)]`, write a program to compute the average score per student using a dictionary.
8. Write a dictionary comprehension to create `{1: 'odd', 2: 'even', 3: 'odd', ...}` for numbers 1 to 10.
9. Write a program to merge two dictionaries where, if a key exists in both, the values are added together.
10. Given a nested dictionary of employees (with `name`, `dept`, `salary`), find the average salary per department.

### Level 3 — Advanced

11. Write a function `flatten_dict(d, sep=".")` that flattens a deeply nested dictionary into a single-level dictionary with dot-separated keys.
12. Implement a word frequency analyser: read a paragraph, count word frequencies, and display the top 5 most frequent words sorted by count descending.
13. Write a program to group a list of words by their sorted letter signature (anagram grouping) — e.g., `"eat"`, `"tea"`, `"ate"` all go in the same group.
14. Implement a simple **in-memory cache** using a dictionary: a function `cached_square(n)` that stores computed squares and returns from cache on repeated calls, printing `"Cache hit"` or `"Computing"` accordingly.
15. Given two dictionaries representing old and new configuration settings, write a program to print: (a) keys added in new config, (b) keys removed from new config, (c) keys whose values changed.

---

*End of Week-02 Day-10 — Python Dictionaries*
