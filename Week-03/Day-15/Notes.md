# Python Full Stack Foundation

# Week-03 – Day-15

# Functional Programming in Python

## Lambda Functions, map(), filter(), reduce(), Comprehensions & Recursion

---

# Learning Objectives

By the end of this session, learners will be able to:

- Understand Functional Programming
- Create Lambda Functions
- Use `map()`
- Use `filter()`
- Use `reduce()`
- Understand Anonymous Functions
- Use List Comprehensions
- Use Dictionary Comprehensions
- Use Set Comprehensions
- Use Generator Expressions
- Apply String Comprehension Techniques
- Understand Recursion
- Solve Interview-Based Programs

---

# Recap

Previously we learned:

- Functions
- Parameters
- Return Values
- Exception Handling
- File Handling

Today we learn Python's Functional Programming concepts that help us write shorter, cleaner, and more efficient code.

---

# 1. What is Functional Programming?

Functional Programming is a programming style in which functions are treated as first-class objects and are used to process data.

Python supports Functional Programming using:

- Lambda Functions
- map()
- filter()
- reduce()
- Comprehensions
- Recursion

---

# Why Functional Programming?

Without Functional Programming

```python
numbers = [1,2,3,4]

result = []

for num in numbers:
    result.append(num * 2)

print(result)
```

Output

```
[2, 4, 6, 8]
```

Using Functional Programming

```python
numbers = [1,2,3,4]

result = list(map(lambda x: x*2, numbers))

print(result)
```

Output

```
[2, 4, 6, 8]
```

Cleaner and shorter.

---

# 2. Lambda Function

## Definition

A **Lambda Function** is a small anonymous function without a name.

It can have:

- Any number of parameters
- Only one expression

---

## Syntax

```python
lambda parameters : expression
```

---

## Normal Function

```python
def square(x):
    return x*x

print(square(5))
```

Output

```
25
```

---

## Equivalent Lambda Function

```python
square = lambda x: x*x

print(square(5))
```

Output

```
25
```

---

## Example 1

Addition

```python
add = lambda a, b: a+b

print(add(10,20))
```

Output

```
30
```

---

## Example 2

Largest Number

```python
largest = lambda a,b: a if a>b else b

print(largest(15,20))
```

Output

```
20
```

---

## Example 3

Even or Odd

```python
check = lambda n: "Even" if n%2==0 else "Odd"

print(check(12))
print(check(15))
```

Output

```
Even
Odd
```

---

# When to Use Lambda?

- Short functions
- Sorting
- map()
- filter()
- reduce()

---

# 3. map() Function

## Definition

Applies a function to every element of an iterable.

---

## Syntax

```python
map(function, iterable)
```

Returns a map object.

Convert it using:

```python
list()
```

---

## Example 1

Square Every Number

```python
numbers = [1,2,3,4,5]

result = list(map(lambda x:x*x, numbers))

print(result)
```

Output

```
[1,4,9,16,25]
```

---

## Example 2

Convert to Uppercase

```python
names = ["alex","john","sam"]

result = list(map(str.upper, names))

print(result)
```

Output

```
['ALEX', 'JOHN', 'SAM']
```

---

## Example 3

Multiply by 10

```python
numbers = [2,4,6]

result = list(map(lambda x:x*10, numbers))

print(result)
```

Output

```
[20,40,60]
```

---

# 4. filter() Function

## Definition

Returns only those elements for which the condition is True.

---

## Syntax

```python
filter(function, iterable)
```

---

## Example 1

Even Numbers

```python
numbers = [1,2,3,4,5,6]

result = list(filter(lambda x:x%2==0, numbers))

print(result)
```

Output

```
[2,4,6]
```

---

## Example 2

Odd Numbers

```python
numbers = [1,2,3,4,5]

result = list(filter(lambda x:x%2!=0, numbers))

print(result)
```

Output

```
[1,3,5]
```

---

## Example 3

Names Longer Than 4 Letters

```python
names = ["Alex","John","Christopher","Sam"]

result = list(filter(lambda x:len(x)>4, names))

print(result)
```

Output

```
['Christopher']
```

---

# 5. reduce() Function

## Definition

Reduces all elements into a single value.

`reduce()` is available in the `functools` module.

---

## Syntax

```python
from functools import reduce

reduce(function, iterable)
```

---

## Example 1

Find Sum

```python
from functools import reduce

numbers = [1,2,3,4,5]

result = reduce(lambda x,y:x+y, numbers)

print(result)
```

Output

```
15
```

---

## Example 2

Find Product

```python
from functools import reduce

numbers = [1,2,3,4]

result = reduce(lambda x,y:x*y, numbers)

print(result)
```

Output

```
24
```

---

# map() vs filter() vs reduce()

| Function | Purpose | Output |
|----------|---------|--------|
| map() | Transform every element | Collection |
| filter() | Select matching elements | Collection |
| reduce() | Combine into one value | Single Value |

---

# 6. List Comprehension

## Definition

A concise way to create lists.

---

## Syntax

```python
[expression for item in iterable]
```

---

## Example 1

Squares

```python
numbers = [x*x for x in range(1,6)]

print(numbers)
```

Output

```
[1,4,9,16,25]
```

---

## Example 2

Even Numbers

```python
numbers = [x for x in range(1,11) if x%2==0]

print(numbers)
```

Output

```
[2,4,6,8,10]
```

---

## Example 3

Uppercase Words

```python
names = ["python","sql","html"]

result = [name.upper() for name in names]

print(result)
```

Output

```
['PYTHON','SQL','HTML']
```

---

# 7. Dictionary Comprehension

## Syntax

```python
{key:value for item in iterable}
```

---

## Example 1

Squares

```python
square = {x:x*x for x in range(1,6)}

print(square)
```

Output

```
{1:1,2:4,3:9,4:16,5:25}
```

---

## Example 2

Word Length

```python
words = ["Python","SQL","HTML"]

length = {word:len(word) for word in words}

print(length)
```

Output

```
{'Python':6,'SQL':3,'HTML':4}
```

---

# 8. Set Comprehension

## Syntax

```python
{expression for item in iterable}
```

---

## Example

```python
numbers = {x*x for x in range(1,6)}

print(numbers)
```

Output

```
{1,4,9,16,25}
```

---

# 9. Generator Expression

Generator expressions generate values one at a time.

---

## Syntax

```python
(expression for item in iterable)
```

---

## Example

```python
numbers = (x*x for x in range(5))

for value in numbers:
    print(value)
```

Output

```
0
1
4
9
16
```

---

# 10. String Comprehension Techniques

Although strings don't have direct comprehensions, we commonly use list comprehensions with `join()`.

---

## Example 1

Uppercase Characters

```python
text = "python"

result = "".join([ch.upper() for ch in text])

print(result)
```

Output

```
PYTHON
```

---

## Example 2

Remove Spaces

```python
text = "P Y T H O N"

result = "".join([ch for ch in text if ch != " "])

print(result)
```

Output

```
PYTHON
```

---

## Example 3

Extract Digits

```python
text = "A1B2C3"

digits = "".join([ch for ch in text if ch.isdigit()])

print(digits)
```

Output

```
123
```

---

# 11. Recursion

## Definition

A function that calls itself is called a **Recursive Function**.

Every recursive function should have:

- Base Case
- Recursive Case

---

## Example 1

Print Numbers 1 to 5

```python
def display(n):

    if n == 6:
        return

    print(n)

    display(n+1)

display(1)
```

Output

```
1
2
3
4
5
```

---

## Example 2

Factorial

```python
def factorial(n):

    if n == 1:
        return 1

    return n * factorial(n-1)

print(factorial(5))
```

Output

```
120
```

---

## Example 3

Sum of Numbers

```python
def total(n):

    if n == 0:
        return 0

    return n + total(n-1)

print(total(5))
```

Output

```
15
```

---

# Iteration vs Recursion

| Iteration | Recursion |
|-----------|-----------|
| Uses loops | Uses function calls |
| Faster | Slightly slower |
| Less memory | More memory |
| Easy for repeated tasks | Useful for tree and divide-and-conquer problems |

---

# 12. Interview Programs

1. Square numbers using `map()`
2. Convert names to uppercase using `map()`
3. Filter even numbers
4. Filter prime numbers (advanced)
5. Find sum using `reduce()`
6. Find product using `reduce()`
7. Create list of squares using comprehension
8. Create cube dictionary using comprehension
9. Create set of vowels
10. Remove spaces from a string
11. Reverse a string using comprehension
12. Count vowels using comprehension
13. Factorial using recursion
14. Fibonacci using recursion
15. Sum of first N numbers using recursion

---

# Quick Summary

| Topic | Purpose |
|--------|---------|
| lambda | Anonymous function |
| map() | Transform elements |
| filter() | Select elements |
| reduce() | Combine elements |
| List Comprehension | Create lists efficiently |
| Dictionary Comprehension | Create dictionaries efficiently |
| Set Comprehension | Create sets efficiently |
| Generator Expression | Generate values lazily |
| String + join() | Build strings efficiently |
| Recursion | Function calling itself |

---

# Homework

1. Create a lambda function to find the square of a number.
2. Use `map()` to double every number in a list.
3. Use `filter()` to select positive numbers.
4. Use `reduce()` to calculate the product of a list.
5. Create a list of even numbers using list comprehension.
6. Create a dictionary of numbers and their cubes.
7. Create a set of squares from 1 to 10.
8. Remove vowels from a string using comprehension.
9. Write a recursive function to find the factorial of a number.
10. Write a recursive function to calculate the sum of first N natural numbers.

---

# Session Summary

Today we learned:

✔ Functional Programming

✔ Lambda Functions

✔ map()

✔ filter()

✔ reduce()

✔ List Comprehensions

✔ Dictionary Comprehensions

✔ Set Comprehensions

✔ Generator Expressions

✔ String Processing using Comprehensions

✔ Recursion

✔ Interview-Oriented Functional Programming Techniques

---

# Next Session Preview
