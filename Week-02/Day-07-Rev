

# Week-02 Day-07: Lists in Python

## Learning Objectives

By the end of this session, students will be able to:

* Define a list
* Create lists
* Access elements using indexing and slicing
* Modify list elements
* Add, remove, and update elements
* Perform mathematical operations on lists
* Use built-in functions
* Use commonly used list methods
* Solve interview-style list programs

---

# 1. What is a List?

### Definition

A **list** is an ordered, mutable (changeable) collection of elements enclosed in square brackets **[]**.

A list can store:

* Integers
* Floats
* Strings
* Booleans
* Other Lists
* Mixed Data Types

---

# 2. Creating Lists

```python
numbers = [10,20,30,40]

names = ["Alex","John","Sam"]

mixed = [10,3.14,"Python",True]

empty = []
```

---

# 3. Checking Data Type

```python
numbers = [10,20,30]

print(type(numbers))
```

---

# 4. Characteristics of Lists

* Ordered
* Mutable
* Allows Duplicates
* Heterogeneous
* Dynamic Size

---

# 5. Accessing List Elements

Elements in a list are accessed using their **index position**.

Python supports two types of indexing:

* **Positive Indexing** (Left → Right)
* **Negative Indexing** (Right → Left)

---

## Example List

```python
numbers = [10, 20, 30, 40, 50]
```

| Element        | 10 | 20 | 30 | 40 | 50 |
| -------------- | -- | -- | -- | -- | -- |
| Positive Index | 0  | 1  | 2  | 3  | 4  |
| Negative Index | -5 | -4 | -3 | -2 | -1 |

---

## Positive Indexing

Positive indexing starts from **0**.

### Example 1

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[0])
print(numbers[2])
print(numbers[4])
```

**Output**

```
10
30
50
```

---

## Negative Indexing

Negative indexing starts from **-1**.

### Example 2

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[-1])
print(numbers[-2])
print(numbers[-5])
```

**Output**

```
50
40
10
```

---

## Accessing Nested Lists

```python
matrix = [
    [10, 20],
    [30, 40]
]

print(matrix[0])
print(matrix[1][0])
```

**Output**

```
[10, 20]
30
```

---

## Invalid Index

Accessing an index that does not exist raises an error.

```python
numbers = [10, 20, 30]

print(numbers[5])
```

**Output**

```
IndexError: list index out of range
```

---

### Important Notes

* Positive indexing starts from **0**.
* Negative indexing starts from **-1**.
* Nested lists use multiple indexes.
* Invalid indexes raise **IndexError**.


---

# 6. List Slicing

List slicing is used to access **multiple elements** from a list.

## Syntax

```python
list_name[start : stop : step]
```

* **start** → Starting index (Included)
* **stop** → Ending index (Excluded)
* **step** → Number of positions to move (Optional)

---

## Example List

```python
numbers = [10, 20, 30, 40, 50, 60]
```

| Element | 10 | 20 | 30 | 40 | 50 | 60 |
| ------- | -- | -- | -- | -- | -- | -- |
| Index   | 0  | 1  | 2  | 3  | 4  | 5  |

---

## Forward Slicing

Move from **Left → Right**.

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[1:4])
print(numbers[:3])
print(numbers[2:])
```

**Output**

```
[20, 30, 40]
[10, 20, 30]
[30, 40, 50, 60]
```

---

## Backward Slicing

Move from **Right → Left** using a negative step.

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[5:1:-1])
```

**Output**

```
[60, 50, 40, 30]
```

---

## Reverse a List

Use `[::-1]` to reverse a list.

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[::-1])
```

**Output**

```
[60, 50, 40, 30, 20, 10]
```

---

## Every Second Element

Use a step value of **2**.

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[::2])
```

**Output**

```
[10, 30, 50]
```

---

## Important Notes

* **start** is included.
* **stop** is excluded.
* Default **step** is `1`.
* Use a negative step (`-1`) for backward slicing.
* `[::-1]` is the easiest way to reverse a list.


---

# 7. Updating List Elements

```python
numbers=[10,20,30]

numbers[1]=200

print(numbers)
```

---

# 8. Adding Elements to a List

Python provides several methods to add elements to a list.

The most commonly used methods are:

* `append()`
* `extend()`
* `insert()`

---

## append()

### Definition

The **append()** method adds **one element** to the **end of the list**.

### Syntax

```python
list_name.append(element)
```

### Example

```python
numbers = [10, 20, 30]

numbers.append(40)

print(numbers)
```

**Output**

```
[10, 20, 30, 40]
```

### Note

* Adds only **one element**.
* Element is added at the **end** of the list.

---

## extend()

### Definition

The **extend()** method adds **multiple elements** (another iterable) to the end of the list.

### Syntax

```python
list_name.extend(iterable)
```

### Example

```python
numbers = [10, 20]

numbers.extend([30, 40])

print(numbers)
```

**Output**

```
[10, 20, 30, 40]
```

### Note

* Adds **multiple elements**.
* Accepts a list, tuple, set, string, etc.

---

## insert()

### Definition

The **insert()** method inserts an element at a specified index.

### Syntax

```python
list_name.insert(index, element)
```

### Example

```python
numbers = [10, 20, 30]

numbers.insert(1, 15)

print(numbers)
```

**Output**

```
[10, 15, 20, 30]
```

### Note

* Adds **one element**.
* Can insert the element **at any position**.

---

# Difference Between append(), extend(), and insert()

| Method     | Adds              | Position            | Example                    |
| ---------- | ----------------- | ------------------- | -------------------------- |
| `append()` | One element       | End of the list     | `numbers.append(40)`       |
| `extend()` | Multiple elements | End of the list     | `numbers.extend([40, 50])` |
| `insert()` | One element       | Any specified index | `numbers.insert(1, 15)`    |


---

# 9. Removing Elements from a List

Python provides several methods to remove elements from a list.

The most commonly used methods are:

* `remove()`
* `pop()`
* `clear()`
* `del` statement

---

## remove()

### Definition

The **remove()** method removes the **first occurrence of a specified value** from the list.

### Syntax

```python
list_name.remove(value)
```

### Example

```python
numbers = [10, 20, 30, 20, 40]

numbers.remove(20)

print(numbers)
```

**Output**

```
[10, 30, 20, 40]
```

### Note

* Removes the **specified value**.
* Removes only the **first occurrence**.
* Raises `ValueError` if the value is not found.

---

## pop()

### Definition

The **pop()** method removes and returns an element at the specified index.

If no index is given, it removes the **last element**.

### Syntax

```python
list_name.pop(index)
```

or

```python
list_name.pop()
```

### Example 1

```python
numbers = [10, 20, 30, 40]

numbers.pop()

print(numbers)
```

**Output**

```
[10, 20, 30]
```

### Example 2

```python
numbers = [10, 20, 30, 40]

numbers.pop(1)

print(numbers)
```

**Output**

```
[10, 30, 40]
```

### Note

* Removes by **index**.
* Returns the removed element.
* Default index is **-1** (last element).

---

## clear()

### Definition

The **clear()** method removes **all elements** from the list.

### Syntax

```python
list_name.clear()
```

### Example

```python
numbers = [10, 20, 30]

numbers.clear()

print(numbers)
```

**Output**

```
[]
```

### Note

* Empties the list.
* The list still exists.

---

## del Statement

### Definition

The **del** statement deletes an element, a slice of elements, or the entire list.

### Example 1: Delete an Element

```python
numbers = [10, 20, 30, 40]

del numbers[1]

print(numbers)
```

**Output**

```
[10, 30, 40]
```

---

### Example 2: Delete the Entire List

```python
numbers = [10, 20, 30]

del numbers

print(numbers)
```

**Output**

```
NameError: name 'numbers' is not defined
```

### Note

* Deletes elements or the complete list.
* After deleting the list, it cannot be accessed.

---

# Difference Between remove(), pop(), clear(), and del

| Method     | Removes                        | Argument             | Returns Value |
| ---------- | ------------------------------ | -------------------- | ------------- |
| `remove()` | Specified value                | Value                | No            |
| `pop()`    | Element at index               | Index (Optional)     | Yes           |
| `clear()`  | All elements                   | None                 | No            |
| `del`      | Element, slice, or entire list | Index / Slice / List | No            |


---
# 10. Mathematical Operators on Lists

Python supports the following mathematical operators on lists:

* `+` (Concatenation)
* `*` (Repetition)

---

## + Operator (Concatenation)

The `+` operator combines two or more lists into a single list.

### Syntax

```python
list1 + list2
```

### Example

```python
a = [1, 2]
b = [3, 4]

print(a + b)
```

**Output**

```text
[1, 2, 3, 4]
```

---

## * Operator (Repetition)

The `*` operator repeats the elements of a list.

### Syntax

```python
list * number
```

### Example

```python
numbers = [1, 2]

print(numbers * 3)
```

**Output**

```text
[1, 2, 1, 2, 1, 2]
```

---

# 11. Membership Operators

Membership operators are used to check whether an element exists in a list.

Python provides two membership operators:

* `in`
* `not in`

---

## in Operator

Returns **True** if the element is present in the list.

### Example

```python
numbers = [10, 20, 30, 40]

print(20 in numbers)
print(50 in numbers)
```

**Output**

```text
True
False
```

---

## not in Operator

Returns **True** if the element is **not present** in the list.

### Example

```python
numbers = [10, 20, 30, 40]

print(50 not in numbers)
print(20 not in numbers)
```

**Output**

```text
True
False
```

---

# 12. Comparison Operators

Lists can be compared using comparison operators.

Python compares lists **element by element** (lexicographical comparison).

---

## Example 1

```python
a = [1, 2]
b = [1, 2]

print(a == b)
```

**Output**

```text
True
```

---

## Example 2

```python
a = [1, 2]
b = [2, 3]

print(a < b)
```

**Output**

```text
True
```

### Explanation

Python compares the first elements of both lists.

* `1 < 2` → `True`

So the entire comparison becomes **True**.

---

## Example 3

```python
a = [5, 10]
b = [5, 20]

print(a < b)
```

**Output**

```text
True
```

### Explanation

* First elements are equal (`5 == 5`)
* Python compares the next elements.
* `10 < 20` → `True`

This type of comparison is called **Lexicographical Comparison**.

---

# 13. Built-in Functions

Python provides several useful built-in functions for lists.

---

## len()

Returns the number of elements in a list.

```python
numbers = [10, 20, 30, 40]

print(len(numbers))
```

**Output**

```text
4
```

---

## max()

Returns the largest element.

```python
numbers = [10, 20, 30, 40]

print(max(numbers))
```

**Output**

```text
40
```

---

## min()

Returns the smallest element.

```python
numbers = [10, 20, 30, 40]

print(min(numbers))
```

**Output**

```text
10
```

---

## sum()

Returns the sum of all numeric elements.

```python
numbers = [10, 20, 30, 40]

print(sum(numbers))
```

**Output**

```text
100
```

---

## sorted()

Returns a new sorted list.

```python
numbers = [40, 10, 30, 20]

print(sorted(numbers))
```

**Output**

```text
[10, 20, 30, 40]
```

---

## list()

Creates a list from another iterable.

```python
text = "Python"

print(list(text))
```

**Output**

```text
['P', 'y', 't', 'h', 'o', 'n']
```

---

# 14. Iterating Through Lists

Iteration means accessing each element of a list one by one.

---

## Using for Loop

```python
numbers = [10, 20, 30, 40]

for num in numbers:
    print(num)
```

**Output**

```text
10
20
30
40
```

---

## Using while Loop

```python
numbers = [10, 20, 30, 40]

i = 0

while i < len(numbers):
    print(numbers[i])
    i += 1
```

**Output**

```text
10
20
30
40
```

---

## Using enumerate()

The `enumerate()` function returns both the **index** and the **value**.

```python
numbers = [10, 20, 30, 40]

for index, value in enumerate(numbers):
    print(index, value)
```

**Output**

```text
0 10
1 20
2 30
3 40
```

---

## Quick Summary

| Concept       | Example              |
| ------------- | -------------------- |
| Concatenation | `list1 + list2`      |
| Repetition    | `list * 3`           |
| Membership    | `10 in numbers`      |
| Comparison    | `[1,2] < [2,3]`      |
| Length        | `len(numbers)`       |
| Largest       | `max(numbers)`       |
| Smallest      | `min(numbers)`       |
| Sum           | `sum(numbers)`       |
| Sort          | `sorted(numbers)`    |
| Iterate       | `for num in numbers` |
| Index + Value | `enumerate(numbers)` |

---

# 15. Popular List Methods

## append()

## extend()

## insert()

## remove()

## pop()

## clear()

## copy()

## count()

## index()

## reverse()

## sort()

---

# 16. Shallow Copy vs Deep Copy (Introduction)

```python
a=[10,20]

b=a

c=a.copy()
```

---

# 17. Nested Lists

```python
matrix=[
[1,2],
[3,4]
]
```

Accessing nested elements.

---

# 18. List Comprehension (Introduction)

```python
numbers=[x*x for x in range(1,6)]
```

---

# 19. Practice Programs (Interview & Logic Building)

### 1. Sum of List Elements

---

### 2. Largest Element

---

### 3. Smallest Element

---

### 4. Second Largest Element

---

### 5. Reverse a List (2 Methods)

---

### 6. Remove Duplicates

---

### 7. Count Even and Odd Numbers

---

### 8. Separate Positive and Negative Numbers

---

### 9. Merge Two Lists

---

### 10. Find Common Elements in Two Lists

---

### 11. Frequency of Each Element

---

### 12. Sort Without Using `sort()`

---

### 13. Rotate List Left by One Position

---

### 14. Rotate List Right by One Position

---

### 15. Check if List is Sorted

---

# Quick Summary Table

| Topic     | Key Concept                |
| --------- | -------------------------- |
| List      | Ordered Mutable Collection |
| Indexing  | Positive & Negative        |
| Slicing   | start:stop:step            |
| append()  | Add one element            |
| extend()  | Add multiple elements      |
| insert()  | Insert at position         |
| remove()  | Remove by value            |
| pop()     | Remove by index            |
| clear()   | Remove all elements        |
| copy()    | Copy list                  |
| count()   | Count occurrences          |
| index()   | Find position              |
| reverse() | Reverse list               |
| sort()    | Sort list                  |
| len()     | Number of elements         |
| max()     | Largest element            |
| min()     | Smallest element           |
| sum()     | Sum of elements            |
| sorted()  | Returns sorted list        |

---

# Self-Study Exercises

1. Find the average of all elements.
2. Remove duplicate values.
3. Find the second largest number.
4. Merge two lists.
5. Reverse a list without slicing.
6. Count positive and negative numbers.
7. Find the frequency of each element.
8. Rotate a list by one position.
9. Check whether a number exists in a list.
10. Create a multiplication table using list comprehension.

This structure mirrors your **Week-02 Day-06 (Strings)** notes, making the course consistent and easy for students to follow. After this, **Week-02 Day-08** can naturally cover **Tuples**, followed by **Sets** and **Dictionaries**.
