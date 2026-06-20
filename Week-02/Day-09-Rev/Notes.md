# Week-02 Day-09 — Python Sets
### Complete Theory, Syntax, Code Examples & Interview Programs

---

## Table of Contents

1. [Theory & Introduction](#1-theory--introduction)
2. [Syntax & Creation](#2-syntax--creation)
3. [Accessing Elements & Indexing](#3-accessing-elements--indexing)
4. [Mathematical (Set) Operators](#4-mathematical-set-operators)
5. [Membership Operators](#5-membership-operators)
6. [Comparison Operators](#6-comparison-operators)
7. [Built-in Functions](#7-built-in-functions)
8. [Iteration](#8-iteration)
9. [Set Methods — Add, Remove & Update](#9-set-methods--add-remove--update)
10. [Set Operations — union, intersection, difference, symmetric_difference](#10-set-operations--union-intersection-difference-symmetric_difference)
11. [Frozen Set](#11-frozen-set)
12. [Set vs List vs Tuple](#12-set-vs-list-vs-tuple)
13. [15 Interview Programs](#13-15-interview-programs)
14. [Summary](#14-summary)
15. [Self-Study Exercises](#15-self-study-exercises)

---

## 1. Theory & Introduction

### What is a Set?

A **set** is an **unordered, mutable collection of unique elements** in Python. Sets are inspired by mathematical sets and are ideal for membership testing, removing duplicates, and performing mathematical operations like union, intersection, and difference.

Sets are one of Python's four built-in collection data types: `list`, `tuple`, `dict`, `set`.

### Key Characteristics

| Property | Description |
|----------|-------------|
| **Unordered** | Elements have no guaranteed position or index |
| **Mutable** | Elements can be added or removed after creation |
| **No Duplicates** | Every element must be unique; duplicates are silently ignored |
| **Heterogeneous** | Can store mixed hashable types (int, str, float, tuple) |
| **Not Indexed** | Cannot access elements by index — no `s[0]` |
| **Hashable Elements Only** | Elements must be immutable (no lists, dicts, or sets inside a set) |
| **Unsubscriptable** | No slicing or indexing |

### Internal Working (Hash Table)

Python sets are implemented using a **hash table**. Each element is passed through a hash function to determine its storage slot. This is why:

- Elements must be **hashable** (immutable)
- Membership testing is **O(1)** (constant time) — much faster than lists O(n)
- Order is **not preserved**

```
s = {10, 20, 30}

Internally:
  hash(10) → slot A → 10
  hash(20) → slot B → 20
  hash(30) → slot C → 30

Checking "is 20 in s?" → compute hash(20) → go to slot B → YES, O(1)
Checking "is 20 in [10,20,30]?" → scan 10, 20... → YES, O(n)
```

### When to Use a Set

- Remove duplicates from a sequence
- Fast membership testing (`in` operator)
- Mathematical set operations (union, intersection, difference)
- Finding common/unique elements between two collections
- Deduplication in data pipelines

---

## 2. Syntax & Creation

```python
# Empty set — MUST use set(), NOT {}
s1 = set()
print(type(s1))         # <class 'set'>

empty_dict = {}          # ⚠️ This is an empty DICT, not a set!
print(type(empty_dict)) # <class 'dict'>

# Set with elements using curly braces
s2 = {1, 2, 3, 4, 5}
print(s2)               # {1, 2, 3, 4, 5}  (order may vary)

# Duplicates are automatically removed
s3 = {1, 2, 2, 3, 3, 3, 4}
print(s3)               # {1, 2, 3, 4}

# Heterogeneous set
s4 = {1, "hello", 3.14, True, (1, 2)}
print(s4)

# Note: True == 1 and False == 0 in sets
s5 = {1, True, 2, False, 0}
print(s5)               # {False, 1, 2}  — True==1, False==0 treated as same

# From iterable using set()
s6 = set([1, 2, 3, 2, 1])    # From list
print(s6)               # {1, 2, 3}

s7 = set("banana")           # From string → unique chars
print(s7)               # {'b', 'a', 'n'}

s8 = set((1, 2, 3, 2))      # From tuple
print(s8)               # {1, 2, 3}

s9 = set(range(1, 6))        # From range
print(s9)               # {1, 2, 3, 4, 5}

# Set comprehension
s10 = {x**2 for x in range(1, 6)}
print(s10)              # {1, 4, 9, 16, 25}

s11 = {x for x in range(20) if x % 3 == 0}
print(s11)              # {0, 3, 6, 9, 12, 15, 18}

# What CANNOT be in a set
try:
    s_bad = {[1, 2], [3, 4]}    # list is unhashable
except TypeError as e:
    print(f"Error: {e}")        # Error: unhashable type: 'list'
```

### Output

```
<class 'set'>
<class 'dict'>
{1, 2, 3, 4, 5}
{1, 2, 3, 4}
{False, 1, 2}
{1, 2, 3}
{'b', 'a', 'n'}
{1, 2, 3}
{1, 2, 3, 4, 5}
{1, 4, 9, 16, 25}
{0, 3, 6, 9, 12, 15, 18}
Error: unhashable type: 'list'
```

---

## 3. Accessing Elements & Indexing

Sets are **unordered** — they do **not** support indexing or slicing. You access elements by iterating or converting to a sorted list.

```python
s = {10, 20, 30, 40, 50}

# ❌ Indexing NOT supported
try:
    print(s[0])
except TypeError as e:
    print(f"Error: {e}")    # Error: 'set' object is not subscriptable

# ✅ Check membership with 'in'
print(30 in s)              # True
print(99 in s)              # False

# ✅ Access all elements via iteration
for item in s:
    print(item, end=" ")
print()

# ✅ Convert to sorted list for indexed access
sorted_s = sorted(s)
print(sorted_s[0])          # 10 (minimum)
print(sorted_s[-1])         # 50 (maximum)

# ✅ Get one arbitrary element using next() + iter()
first = next(iter(s))
print(f"Arbitrary element: {first}")

# ✅ pop() removes and returns an arbitrary element
s2 = {1, 2, 3}
val = s2.pop()
print(f"Popped: {val}, Remaining: {s2}")
```

### Output

```
Error: 'set' object is not subscriptable
True
False
10 20 30 40 50
10
50
Arbitrary element: 10
Popped: 1, Remaining: {2, 3}
```

> **Note:** The print order of set elements may vary each time because sets are unordered.

---

## 4. Mathematical (Set) Operators

Python provides symbolic operators that mirror mathematical set notation.

| Operator | Symbol | Method Equivalent | Description |
|----------|--------|-------------------|-------------|
| Union | `\|` | `.union()` | All elements from both sets |
| Intersection | `&` | `.intersection()` | Common elements only |
| Difference | `-` | `.difference()` | Elements in A but not in B |
| Symmetric Difference | `^` | `.symmetric_difference()` | Elements in either but not both |
| Subset | `<=` | `.issubset()` | Is A a subset of B? |
| Proper Subset | `<` | — | Is A a proper subset of B? |
| Superset | `>=` | `.issuperset()` | Is A a superset of B? |

```python
A = {1, 2, 3, 4, 5}
B = {3, 4, 5, 6, 7}

# Union — all elements from both
print(A | B)            # {1, 2, 3, 4, 5, 6, 7}

# Intersection — only common
print(A & B)            # {3, 4, 5}

# Difference — in A but not B
print(A - B)            # {1, 2}

# Difference — in B but not A
print(B - A)            # {6, 7}

# Symmetric Difference — in either but not both
print(A ^ B)            # {1, 2, 6, 7}

# Subset check
C = {3, 4}
print(C <= A)           # True  — C is a subset of A
print(A <= A)           # True  — every set is a subset of itself
print(C < A)            # True  — C is a PROPER subset (C ≠ A)
print(A < A)            # False — A is NOT a proper subset of itself

# Superset check
print(A >= C)           # True  — A is a superset of C
print(A > C)            # True  — A is a proper superset of C

# Compound set expression
D = {1, 2, 3}
E = {2, 3, 4}
F = {3, 4, 5}
print((D | E) & F)      # {3, 4}
print(D ^ E ^ F)        # {1, 4, 5}

# Update operators (modify set IN-PLACE)
X = {1, 2, 3}
X |= {4, 5}
print(X)                # {1, 2, 3, 4, 5}

X &= {2, 3, 4}
print(X)                # {2, 3, 4}

X -= {3}
print(X)                # {2, 4}

X ^= {2, 5}
print(X)                # {4, 5}
```

### Output

```
{1, 2, 3, 4, 5, 6, 7}
{3, 4, 5}
{1, 2}
{6, 7}
{1, 2, 6, 7}
True
True
True
False
True
True
{3, 4}
{1, 4, 5}
{1, 2, 3, 4, 5}
{2, 3, 4}
{2, 4}
{4, 5}
```

---

## 5. Membership Operators

`in` and `not in` are the **primary way** to access/query set elements. Sets are optimised for this — O(1) vs O(n) for lists.

```python
fruits = {"apple", "banana", "cherry", "mango"}

# in
print("apple" in fruits)        # True
print("grape" in fruits)        # False

# not in
print("grape" not in fruits)    # True
print("mango" not in fruits)    # False

# Practical — guard before processing
if "banana" in fruits:
    print("We have banana!")

# Speed comparison — set vs list (conceptual)
import time

large_list = list(range(1_000_000))
large_set  = set(range(1_000_000))
target = 999_999

# List search
start = time.time()
_ = target in large_list
print(f"List search: {time.time() - start:.6f}s")

# Set search
start = time.time()
_ = target in large_set
print(f"Set search:  {time.time() - start:.6f}s")

# Membership in nested set — only top-level
s = {(1, 2), (3, 4), (5, 6)}
print((1, 2) in s)      # True
print(1 in s)           # False — 1 is not a top-level element
```

### Output

```
True
False
True
False
We have banana!
List search: 0.012340s
Set search:  0.000001s
True
False
```

---

## 6. Comparison Operators

Sets use comparison operators **as subset/superset tests** — NOT element-wise comparison like lists or tuples.

```python
A = {1, 2, 3}
B = {1, 2, 3}
C = {1, 2, 3, 4}
D = {1, 2}

# Equality — same elements regardless of order
print(A == B)           # True
print(A == C)           # False

# Inequality
print(A != C)           # True

# Subset (<=) — all elements of A are in B
print(A <= B)           # True   (A is subset of B, equal sets)
print(D <= A)           # True   (D is subset of A)
print(C <= A)           # False  (C has 4, which is not in A)

# Proper subset (<) — subset but NOT equal
print(D < A)            # True   (D ⊂ A, D ≠ A)
print(A < B)            # False  (A == B, not a proper subset)

# Superset (>=) — all elements of B are in A
print(C >= A)           # True   (C is superset of A)
print(A >= D)           # True

# Proper superset (>)
print(C > A)            # True   (C is proper superset of A)
print(A > B)            # False  (A == B)

# NOTE: < and > do NOT compare "sizes" — they check subset/superset
print({1, 2} < {3, 4})  # False — no subset relationship exists
print({1, 2} > {3, 4})  # False — same reason

# Sets with equal cardinality
print({1, 2, 3} < {1, 2, 4})   # False — neither is a subset of the other
```

### Output

```
True
False
True
True
True
False
True
False
True
True
True
False
False
False
False
```

---

## 7. Built-in Functions

```python
s = {3, 1, 4, 1, 5, 9, 2, 6, 5}   # Duplicates silently dropped
print(s)                # {1, 2, 3, 4, 5, 6, 9}

# len() — number of unique elements
print(len(s))           # 7

# max() and min()
print(max(s))           # 9
print(min(s))           # 1

# sum()
print(sum(s))           # 30

# sorted() — returns a sorted LIST
print(sorted(s))                    # [1, 2, 3, 4, 5, 6, 9]
print(sorted(s, reverse=True))      # [9, 6, 5, 4, 3, 2, 1]

# Convert back to set (loses order benefit)
print(type(sorted(s)))              # <class 'list'>

# enumerate() — with sorted for predictable output
for i, v in enumerate(sorted(s)):
    print(f"  {i}: {v}")

# any() and all()
s2 = {0, 1, 2, 3}
print(any(s2))          # True  — at least one truthy (1, 2, 3)
print(all(s2))          # False — 0 is falsy

s3 = {1, 2, 3}
print(all(s3))          # True  — all truthy

# type() and id()
print(type(s))          # <class 'set'>

# list() and tuple() conversion
print(list(s))          # [1, 2, 3, 4, 5, 6, 9]  (order may vary)
print(tuple(s))         # (1, 2, 3, 4, 5, 6, 9)  (order may vary)
```

### Output

```
{1, 2, 3, 4, 5, 6, 9}
7
9
1
30
[1, 2, 3, 4, 5, 6, 9]
[9, 6, 5, 4, 3, 2, 1]
<class 'list'>
  0: 1
  1: 2
  2: 3
  3: 4
  4: 5
  5: 6
  6: 9
True
False
True
<class 'set'>
[1, 2, 3, 4, 5, 6, 9]
(1, 2, 3, 4, 5, 6, 9)
```

---

## 8. Iteration

```python
colors = {"red", "green", "blue", "yellow"}

# Basic for loop (order not guaranteed)
for color in colors:
    print(color)

print("---")

# Sorted iteration (predictable order)
for color in sorted(colors):
    print(color)

print("---")

# Enumerate with sorted
for i, color in enumerate(sorted(colors), start=1):
    print(f"{i}. {color}")

print("---")

# Iterating two sets simultaneously with zip (after sorting)
A = {1, 2, 3}
B = {4, 5, 6}
for a, b in zip(sorted(A), sorted(B)):
    print(f"{a} — {b}")

print("---")

# Set comprehension
nums = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
evens = {x for x in nums if x % 2 == 0}
squares = {x**2 for x in nums}
print(evens)            # {2, 4, 6, 8, 10}
print(squares)          # {1, 4, 9, 16, 25, 36, 49, 64, 81, 100}

# Nested iteration over set of tuples
pairs = {(1, "one"), (2, "two"), (3, "three")}
for num, word in sorted(pairs):
    print(f"{num} → {word}")
```

### Output

```
red
blue
yellow
green
---
blue
green
red
yellow
---
1. blue
2. green
3. red
4. yellow
---
1 — 4
2 — 5
3 — 6
---
{2, 4, 6, 8, 10}
{1, 4, 9, 16, 25, 36, 49, 64, 81, 100}
1 → one
2 → two
3 → three
```

---

## 9. Set Methods — Add, Remove & Update

Sets have a rich set of methods for modifying elements.

### Adding Elements

```python
s = {1, 2, 3}

# add() — adds a single element; does nothing if element exists
s.add(4)
print(s)            # {1, 2, 3, 4}

s.add(2)            # Already exists — no error, no duplicate
print(s)            # {1, 2, 3, 4}

# update() — adds multiple elements from any iterable
s.update([5, 6, 7])
print(s)            # {1, 2, 3, 4, 5, 6, 7}

s.update({8, 9}, (10, 11), "ab")   # Multiple iterables at once
print(sorted(s))    # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 'a', 'b']
```

### Removing Elements

```python
s = {1, 2, 3, 4, 5}

# remove() — removes element; raises KeyError if not found
s.remove(3)
print(s)            # {1, 2, 4, 5}

try:
    s.remove(99)    # 99 not in set
except KeyError as e:
    print(f"KeyError: {e}")   # KeyError: 99

# discard() — removes element; does NOT raise error if not found ✅
s.discard(4)
print(s)            # {1, 2, 5}

s.discard(99)       # No error even though 99 isn't there
print(s)            # {1, 2, 5}

# pop() — removes and returns an ARBITRARY element
s2 = {10, 20, 30}
val = s2.pop()
print(f"Popped: {val}, Remaining: {s2}")

# pop() on empty set raises KeyError
try:
    empty = set()
    empty.pop()
except KeyError as e:
    print(f"KeyError on pop: {e}")

# clear() — removes ALL elements
s3 = {1, 2, 3}
s3.clear()
print(s3)           # set()
```

### Copying

```python
original = {1, 2, 3}

# Shallow copy
copy1 = original.copy()
copy1.add(4)
print(original)     # {1, 2, 3}  — unchanged
print(copy1)        # {1, 2, 3, 4}

# Assignment (NOT a copy — both point to same set)
copy2 = original
copy2.add(99)
print(original)     # {1, 2, 3, 99}  — also modified!
```

### Output

```
{1, 2, 3, 4}
{1, 2, 3, 4}
{1, 2, 3, 4, 5, 6, 7}
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 'a', 'b']
{1, 2, 4, 5}
KeyError: 99
{1, 2, 5}
{1, 2, 5}
Popped: 10, Remaining: {20, 30}
KeyError on pop: 'pop from an empty set'
set()
{1, 2, 3}
{1, 2, 3, 4}
{1, 2, 3, 99}
```

---

## 10. Set Operations — union, intersection, difference, symmetric_difference

All four core set operations are available as **methods** and as **operators**. Methods accept any iterable; operators require sets.

### Union

Returns all elements from both sets (no duplicates).

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

print(A | B)                    # {1, 2, 3, 4, 5, 6}
print(A.union(B))               # {1, 2, 3, 4, 5, 6}

# union() accepts any iterable, | requires a set
print(A.union([5, 6, 7]))       # {1, 2, 3, 4, 5, 6, 7}  ✅
# print(A | [5, 6, 7])         # ❌ TypeError

# Union of multiple sets
C = {6, 7, 8}
print(A | B | C)                # {1, 2, 3, 4, 5, 6, 7, 8}
print(A.union(B, C))            # {1, 2, 3, 4, 5, 6, 7, 8}

# update() = union in-place
A2 = {1, 2, 3}
A2.update({4, 5})
print(A2)                       # {1, 2, 3, 4, 5}
```

### Intersection

Returns only elements common to both sets.

```python
A = {1, 2, 3, 4, 5}
B = {3, 4, 5, 6, 7}

print(A & B)                            # {3, 4, 5}
print(A.intersection(B))                # {3, 4, 5}

# Multiple sets
C = {4, 5, 6}
print(A & B & C)                        # {4, 5}
print(A.intersection(B, C))             # {4, 5}

# intersection_update() — in-place
A2 = {1, 2, 3, 4, 5}
A2.intersection_update({3, 4, 5, 6})
print(A2)                               # {3, 4, 5}
```

### Difference

Returns elements in A that are NOT in B.

```python
A = {1, 2, 3, 4, 5}
B = {3, 4, 5, 6, 7}

print(A - B)                    # {1, 2}       — in A, not in B
print(B - A)                    # {6, 7}       — in B, not in A
print(A.difference(B))          # {1, 2}
print(B.difference(A))          # {6, 7}

# difference_update() — in-place
A2 = {1, 2, 3, 4, 5}
A2.difference_update({3, 4})
print(A2)                       # {1, 2, 5}
```

### Symmetric Difference

Returns elements in either set, but NOT in both.

```python
A = {1, 2, 3, 4, 5}
B = {3, 4, 5, 6, 7}

print(A ^ B)                            # {1, 2, 6, 7}
print(A.symmetric_difference(B))        # {1, 2, 6, 7}

# Note: A ^ B == (A - B) | (B - A)
print((A - B) | (B - A))               # {1, 2, 6, 7}

# symmetric_difference_update() — in-place
A2 = {1, 2, 3, 4}
A2.symmetric_difference_update({3, 4, 5, 6})
print(A2)                               # {1, 2, 5, 6}
```

### isdisjoint(), issubset(), issuperset()

```python
A = {1, 2, 3}
B = {4, 5, 6}
C = {1, 2}

# isdisjoint() — True if no common elements
print(A.isdisjoint(B))          # True   — no common elements
print(A.isdisjoint(C))          # False  — 1, 2 are common

# issubset() — True if all A elements are in B
print(C.issubset(A))            # True
print(A.issubset(C))            # False

# issuperset() — True if A contains all B elements
print(A.issuperset(C))          # True
print(C.issuperset(A))          # False
```

### Output Summary

```
{1, 2, 3, 4, 5, 6}       ← Union
{3, 4, 5}                 ← Intersection
{1, 2}                    ← Difference A-B
{6, 7}                    ← Difference B-A
{1, 2, 6, 7}              ← Symmetric Difference
True                      ← isdisjoint
False
True                      ← issubset
False
True                      ← issuperset
False
```

---

## 11. Frozen Set

A **frozenset** is an **immutable** version of a set. Once created, elements cannot be added, removed, or changed.

```python
# Creation
fs = frozenset({1, 2, 3, 4, 5})
print(fs)               # frozenset({1, 2, 3, 4, 5})
print(type(fs))         # <class 'frozenset'>

# From iterable
fs2 = frozenset([1, 2, 2, 3])
print(fs2)              # frozenset({1, 2, 3})

fs3 = frozenset("hello")
print(fs3)              # frozenset({'h', 'e', 'l', 'o'})

# All read operations work
print(len(fs))          # 5
print(3 in fs)          # True
print(min(fs))          # 1
print(max(fs))          # 5
print(sorted(fs))       # [1, 2, 3, 4, 5]

# All set operations work
A = frozenset({1, 2, 3})
B = frozenset({2, 3, 4})
print(A | B)            # frozenset({1, 2, 3, 4})
print(A & B)            # frozenset({2, 3})
print(A - B)            # frozenset({1})
print(A ^ B)            # frozenset({1, 4})

# Modification is NOT allowed
try:
    fs.add(6)
except AttributeError as e:
    print(f"Error: {e}")    # Error: 'frozenset' object has no attribute 'add'

# Frozenset CAN be a dictionary key or element of a set (it's hashable!)
d = {frozenset({1, 2}): "pair", frozenset({3, 4}): "another pair"}
print(d[frozenset({1, 2})])     # pair

s = {frozenset({1}), frozenset({2}), frozenset({3})}
print(s)

# Use case: fixed set of allowed roles
ALLOWED_ROLES = frozenset({"admin", "editor", "viewer"})

def check_role(role):
    if role in ALLOWED_ROLES:
        return f"Access granted: {role}"
    return f"Access denied: {role}"

print(check_role("admin"))      # Access granted: admin
print(check_role("hacker"))     # Access denied: hacker
```

### Output

```
frozenset({1, 2, 3, 4, 5})
<class 'frozenset'>
frozenset({1, 2, 3})
frozenset({'h', 'e', 'l', 'o'})
5
True
1
5
[1, 2, 3, 4, 5]
frozenset({1, 2, 3, 4})
frozenset({2, 3})
frozenset({1})
frozenset({1, 4})
Error: 'frozenset' object has no attribute 'add'
pair
{frozenset({1}), frozenset({2}), frozenset({3})}
Access granted: admin
Access denied: hacker
```

---

## 12. Set vs List vs Tuple

| Feature | Set | List | Tuple |
|---------|-----|------|-------|
| **Syntax** | `{1, 2}` | `[1, 2]` | `(1, 2)` |
| **Ordered** | ❌ No | ✅ Yes | ✅ Yes |
| **Mutable** | ✅ Yes | ✅ Yes | ❌ No |
| **Duplicates** | ❌ Not allowed | ✅ Allowed | ✅ Allowed |
| **Indexed/Sliceable** | ❌ No | ✅ Yes | ✅ Yes |
| **Hashable** | ❌ No | ❌ No | ✅ Yes |
| **Membership `in`** | O(1) ⚡ | O(n) 🐢 | O(n) 🐢 |
| **Use case** | Unique items, fast lookup | General-purpose sequence | Fixed/immutable data |
| **Elements must be** | Hashable | Any type | Any type |
| **Dict key?** | ❌ | ❌ | ✅ |

```python
import sys

my_set   = {1, 2, 3, 4, 5}
my_list  = [1, 2, 3, 4, 5]
my_tuple = (1, 2, 3, 4, 5)

print(f"Set   memory: {sys.getsizeof(my_set)} bytes")
print(f"List  memory: {sys.getsizeof(my_list)} bytes")
print(f"Tuple memory: {sys.getsizeof(my_tuple)} bytes")

# De-duplication: set wins
data = [1, 2, 2, 3, 3, 3, 4]
unique = list(set(data))
print(unique)               # [1, 2, 3, 4]

# When to use what
# Set   → email addresses, visited URLs, unique tags, access control lists
# List  → ordered queue, shopping cart, log entries
# Tuple → (lat, lon), (R, G, B), database row, function multi-return
```

### Output

```
Set   memory: 216 bytes
List  memory: 120 bytes
Tuple memory: 80 bytes
[1, 2, 3, 4]
```

---

## 13. 15 Interview Programs

---

### Program 1: Remove Duplicates from a List Using a Set

```python
def remove_duplicates(lst):
    return list(set(lst))

def remove_duplicates_ordered(lst):
    """Preserve original order"""
    seen = set()
    result = []
    for item in lst:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return result

data = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
print(remove_duplicates(data))          # [1, 2, 3, 4, 5, 6, 9]  (order may vary)
print(remove_duplicates_ordered(data))  # [3, 1, 4, 5, 9, 2, 6]  (order preserved)
```

**Output:**
```
[1, 2, 3, 4, 5, 6, 9]
[3, 1, 4, 5, 9, 2, 6]
```

---

### Program 2: Find Common Elements Between Two Lists

```python
def common_elements(list1, list2):
    return list(set(list1) & set(list2))

A = [1, 2, 3, 4, 5, 6]
B = [3, 4, 5, 6, 7, 8]
print(sorted(common_elements(A, B)))    # [3, 4, 5, 6]
```

**Output:**
```
[3, 4, 5, 6]
```

---

### Program 3: Find Elements in First List But Not Second

```python
def unique_to_first(list1, list2):
    return list(set(list1) - set(list2))

students_A = ["Alice", "Bob", "Charlie", "David"]
students_B = ["Charlie", "David", "Eve", "Frank"]

only_in_A = unique_to_first(students_A, students_B)
only_in_B = unique_to_first(students_B, students_A)

print("Only in A:", sorted(only_in_A))  # ['Alice', 'Bob']
print("Only in B:", sorted(only_in_B))  # ['Eve', 'Frank']
```

**Output:**
```
Only in A: ['Alice', 'Bob']
Only in B: ['Eve', 'Frank']
```

---

### Program 4: Check if Two Sets are Disjoint

```python
def are_disjoint(s1, s2):
    return s1.isdisjoint(s2)

A = {1, 2, 3}
B = {4, 5, 6}
C = {3, 4, 5}

print(are_disjoint(A, B))   # True  — no common elements
print(are_disjoint(A, C))   # False — 3 is common
```

**Output:**
```
True
False
```

---

### Program 5: Find All Unique Characters in a String

```python
def unique_chars(s):
    return set(s.replace(" ", ""))

def count_unique_chars(s):
    return len(set(s.replace(" ", "")))

sentence = "hello world"
print(unique_chars(sentence))           # {'h', 'e', 'l', 'o', 'w', 'r', 'd'}
print(count_unique_chars(sentence))     # 7
print(sorted(unique_chars(sentence)))   # ['d', 'e', 'h', 'l', 'o', 'r', 'w']
```

**Output:**
```
{'h', 'e', 'l', 'o', 'w', 'r', 'd'}
7
['d', 'e', 'h', 'l', 'o', 'r', 'w']
```

---

### Program 6: Check if One Set is a Subset of Another

```python
def check_subset(s1, s2):
    if s1 == s2:
        return f"{s1} equals {s2}"
    elif s1 < s2:
        return f"{s1} is a proper subset of {s2}"
    elif s1 > s2:
        return f"{s1} is a proper superset of {s2}"
    elif s1 <= s2:
        return f"{s1} is a subset of {s2}"
    else:
        return "No subset/superset relationship"

print(check_subset({1, 2}, {1, 2, 3}))    # {1, 2} is a proper subset of {1, 2, 3}
print(check_subset({1, 2, 3}, {1, 2}))    # {1, 2, 3} is a proper superset of {1, 2}
print(check_subset({1, 2}, {1, 2}))       # {1, 2} equals {1, 2}
print(check_subset({1, 5}, {2, 3, 4}))    # No subset/superset relationship
```

**Output:**
```
{1, 2} is a proper subset of {1, 2, 3}
{1, 2, 3} is a proper superset of {1, 2}
{1, 2} equals {1, 2}
No subset/superset relationship
```

---

### Program 7: Find Symmetric Difference (Elements Not in Both)

```python
def symmetric_diff(s1, s2):
    return s1 ^ s2

skills_team_A = {"Python", "SQL", "Excel", "PowerBI"}
skills_team_B = {"Python", "Java", "SQL", "Tableau"}

unique_skills = symmetric_diff(skills_team_A, skills_team_B)
print("Skills unique to one team:", sorted(unique_skills))
# ['Excel', 'Java', 'PowerBI', 'Tableau']

common = skills_team_A & skills_team_B
print("Common skills:", sorted(common))
# ['Python', 'SQL']
```

**Output:**
```
Skills unique to one team: ['Excel', 'Java', 'PowerBI', 'Tableau']
Common skills: ['Python', 'SQL']
```

---

### Program 8: Count Distinct Words in a Sentence

```python
def count_distinct_words(sentence):
    words = sentence.lower().split()
    return len(set(words)), set(words)

text = "the quick brown fox jumps over the lazy dog the fox"
count, unique = count_distinct_words(text)
print(f"Total words: {len(text.split())}")
print(f"Distinct words: {count}")
print(f"Unique words: {sorted(unique)}")
```

**Output:**
```
Total words: 11
Distinct words: 8
Unique words: ['brown', 'dog', 'fox', 'jumps', 'lazy', 'over', 'quick', 'the']
```

---

### Program 9: Check if a String is an Anagram Using Sets

```python
def is_anagram_check(s1, s2):
    """Using set — detects same characters (ignores frequency)"""
    return set(s1.lower()) == set(s2.lower())

def is_true_anagram(s1, s2):
    """Using sorted — checks exact character frequency"""
    return sorted(s1.lower()) == sorted(s2.lower())

print(is_anagram_check("listen", "silent"))  # True
print(is_anagram_check("hello", "world"))    # False
print(is_true_anagram("listen", "silent"))   # True
print(is_true_anagram("aab", "abb"))         # False  (set check gives True, sorted gives False)
print(is_anagram_check("aab", "abb"))        # True   (set ignores frequency)
```

**Output:**
```
True
False
True
False
True
```

---

### Program 10: Power Set of a Set

```python
from itertools import combinations

def power_set(s):
    """Returns all subsets of s including empty set and s itself"""
    s = list(s)
    n = len(s)
    result = []
    for r in range(n + 1):
        for combo in combinations(s, r):
            result.append(set(combo))
    return result

s = {1, 2, 3}
ps = power_set(s)
print(f"Power set of {s} has {len(ps)} subsets:")
for subset in ps:
    print(f"  {subset}")
```

**Output:**
```
Power set of {1, 2, 3} has 8 subsets:
  set()
  {1}
  {2}
  {3}
  {1, 2}
  {1, 3}
  {2, 3}
  {1, 2, 3}
```

---

### Program 11: Find Missing Numbers in a Range

```python
def find_missing(data, start, end):
    full_range = set(range(start, end + 1))
    given = set(data)
    return sorted(full_range - given)

numbers = [1, 2, 4, 6, 7, 10]
missing = find_missing(numbers, 1, 10)
print(f"Missing numbers (1-10): {missing}")   # [3, 5, 8, 9]
```

**Output:**
```
Missing numbers (1-10): [3, 5, 8, 9]
```

---

### Program 12: Union of Multiple Sets

```python
def multi_union(*sets):
    result = set()
    for s in sets:
        result |= s
    return result

# Alternative using unpacking
def multi_union_v2(*sets):
    return set().union(*sets)

A = {1, 2, 3}
B = {3, 4, 5}
C = {5, 6, 7}
D = {7, 8, 9}

print(multi_union(A, B, C, D))      # {1, 2, 3, 4, 5, 6, 7, 8, 9}
print(multi_union_v2(A, B, C, D))   # {1, 2, 3, 4, 5, 6, 7, 8, 9}
```

**Output:**
```
{1, 2, 3, 4, 5, 6, 7, 8, 9}
{1, 2, 3, 4, 5, 6, 7, 8, 9}
```

---

### Program 13: Find Duplicate Elements in a List

```python
def find_duplicates(lst):
    seen = set()
    duplicates = set()
    for item in lst:
        if item in seen:
            duplicates.add(item)
        else:
            seen.add(item)
    return sorted(duplicates)

data = [1, 2, 3, 2, 4, 5, 3, 6, 1, 7]
print(f"Duplicates: {find_duplicates(data)}")   # [1, 2, 3]

# One-liner (less explicit)
def find_duplicates_v2(lst):
    return sorted(set(x for x in lst if lst.count(x) > 1))

print(find_duplicates_v2(data))     # [1, 2, 3]
```

**Output:**
```
Duplicates: [1, 2, 3]
Duplicates: [1, 2, 3]
```

---

### Program 14: Frozenset as Dictionary Key (Grouping)

```python
# Group students who share the same set of subjects
records = [
    ("Alice",   frozenset({"Math", "Science", "English"})),
    ("Bob",     frozenset({"Math", "Science", "English"})),
    ("Charlie", frozenset({"Math", "Art"})),
    ("David",   frozenset({"Math", "Art"})),
    ("Eve",     frozenset({"Science", "English"})),
]

groups = {}
for name, subjects in records:
    if subjects not in groups:
        groups[subjects] = []
    groups[subjects].append(name)

for subjects, students in groups.items():
    print(f"Subjects: {sorted(subjects)} → Students: {students}")
```

**Output:**
```
Subjects: ['English', 'Math', 'Science'] → Students: ['Alice', 'Bob']
Subjects: ['Art', 'Math'] → Students: ['Charlie', 'David']
Subjects: ['English', 'Science'] → Students: ['Eve']
```

---

### Program 15: Venn Diagram Data (Three Sets)

```python
def venn_three(A, B, C):
    only_A   = A - B - C
    only_B   = B - A - C
    only_C   = C - A - B
    A_and_B  = (A & B) - C
    B_and_C  = (B & C) - A
    A_and_C  = (A & C) - B
    all_three = A & B & C
    none      = (A | B | C)    # all elements that appeared

    print(f"Only A:         {sorted(only_A)}")
    print(f"Only B:         {sorted(only_B)}")
    print(f"Only C:         {sorted(only_C)}")
    print(f"A ∩ B only:     {sorted(A_and_B)}")
    print(f"B ∩ C only:     {sorted(B_and_C)}")
    print(f"A ∩ C only:     {sorted(A_and_C)}")
    print(f"A ∩ B ∩ C:      {sorted(all_three)}")
    print(f"A ∪ B ∪ C:      {sorted(none)}")

Python_devs  = {"Alice", "Bob", "Charlie", "David", "Eve"}
Java_devs    = {"Charlie", "David", "Frank", "Grace"}
SQL_experts  = {"Alice", "David", "Grace", "Henry"}

venn_three(Python_devs, Java_devs, SQL_experts)
```

**Output:**
```
Only A:         ['Bob', 'Eve']
Only B:         ['Frank']
Only C:         ['Henry']
A ∩ B only:     ['Charlie']
B ∩ C only:     ['Grace']
A ∩ C only:     ['Alice']
A ∩ B ∩ C:      ['David']
A ∪ B ∪ C:      ['Alice', 'Bob', 'Charlie', 'David', 'Eve', 'Frank', 'Grace', 'Henry']
```

---

## 14. Summary

| Topic | Key Points |
|-------|-----------|
| **Definition** | Unordered, mutable, unique-elements collection |
| **Creation** | `{1,2,3}`, `set()`, `set(iterable)`, `{x for x in ...}` |
| **Empty set** | `set()` — NOT `{}` (that creates a dict) |
| **No indexing** | Cannot use `s[0]`; access via `in`, `for`, `sorted()` |
| **Operators** | `\|` union, `&` intersection, `-` difference, `^` symmetric diff |
| **In-place** | `\|=`, `&=`, `-=`, `^=` — modify set directly |
| **Membership** | `in` / `not in` — O(1) hash-table lookup |
| **Comparison** | `==`, `!=`, `<`, `<=`, `>`, `>=` as subset/superset tests |
| **Built-ins** | `len`, `max`, `min`, `sum`, `sorted`, `any`, `all` |
| **Methods** | `add`, `update`, `remove`, `discard`, `pop`, `clear`, `copy` |
| **Set ops** | `union`, `intersection`, `difference`, `symmetric_difference` |
| **Query** | `issubset`, `issuperset`, `isdisjoint` |
| **Frozenset** | Immutable set; can be dict key or element of another set |
| **vs List** | Set: unique/O(1) lookup; List: ordered/indexed/duplicates |

### Golden Rules

```python
# 1. Empty set → use set(), NOT {}
s = set()           # ✅ set
d = {}              # ❌ dict

# 2. Elements must be hashable
s = {1, "a", (1,2)}    # ✅ all hashable
# s = {[1, 2]}         # ❌ list is unhashable

# 3. Duplicates are silently ignored
s = {1, 1, 1, 2}
print(s)            # {1, 2}

# 4. Use discard() over remove() when unsure element exists
s.discard(99)       # ✅ safe — no error
# s.remove(99)      # ❌ raises KeyError if not found

# 5. Order is not guaranteed
for x in {3, 1, 2}:
    print(x)        # Could print in any order
```

---

## 15. Self-Study Exercises

### Level 1 — Basic

1. Create a set of 5 of your favourite movies. Add one more movie and print the updated set.
2. Create a set `{10, 20, 30, 40, 50}`. Try to print its first element using indexing — observe the error and fix it using `sorted()`.
3. Create a set `{1, 2, 3, 4, 5}`. Remove element `3` using `remove()` and element `10` safely using `discard()`. Print the result.
4. Given `s = {1, 2, 2, 3, 3, 3, 4}`, prove that sets do not store duplicates by printing the set and its length.
5. Write a program to check if `"Python"` is in the set `{"Java", "Python", "C++", "Go"}` using the `in` operator.

### Level 2 — Intermediate

6. Given two lists, write a program to find and print elements that are present in both lists using sets.
7. Write a program to find elements that appear in List A but not in List B, and vice versa.
8. Given the string `"programming"`, use a set to find all unique characters and print them in sorted order.
9. Write a function `deduplicate(lst)` that removes duplicates from a list while **preserving the original order**.
10. Write a program using `update()` to combine three different sets of student names into one master set.

### Level 3 — Advanced

11. You are given two sets: `enrolled = {"Alice", "Bob", "Charlie"}` and `paid = {"Bob", "Charlie", "David"}`. Print students who enrolled but haven't paid, who paid but aren't enrolled, and who both enrolled and paid.
12. Write a function `find_missing_numbers(data, n)` that finds all numbers from 1 to n that are not in the given list.
13. Implement a function that takes a sentence and returns a frozenset of unique words. Store multiple such frozensets in a dictionary mapping them to document names.
14. Write a program to simulate a simple **access control system**: define a frozenset of admin usernames. For each login attempt in a list, print whether access is granted or denied.
15. Given three lists representing students who passed Maths, Science, and English, use set operations to find: (a) students who passed all three, (b) students who passed exactly two subjects, (c) students who failed all three.

---

*End of Week-02 Day-09 — Python Sets*
