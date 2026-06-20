# Week 2 -- Day 06: Strings in Python

## Learning Objectives

By the end of this session, students will be able to:

-   Define a string in Python.
-   Create single-line and multi-line strings.
-   Access characters using indexing and slicing.
-   Perform mathematical and comparison operations on strings.
-   Use built-in functions and operators.
-   Apply commonly used string methods.

------------------------------------------------------------------------

# 1. What is a String?

### Definition

A **string** is a sequence of characters enclosed in **single quotes ('
')** or **double quotes (" ")**.

A string may contain:

-   Letters
-   Numbers
-   Spaces
-   Special characters

### Syntax

``` python
name = "Alex"
city = 'Hyderabad'

print(name)
print(city)
```

**Output**

    Alex
    Hyderabad

------------------------------------------------------------------------

# 2. Checking the Data Type

Use the **type()** function.

``` python
name = "Python"

print(type(name))
```

**Output**

    <class 'str'>

------------------------------------------------------------------------

# 3. Multi-line Strings

Use triple quotes.

### Triple Single Quotes

``` python
text = '''
Welcome
to
Python
'''

print(text)
```

### Triple Double Quotes

``` python
text = """
Learning
Python
is Fun
"""

print(text)
```

------------------------------------------------------------------------

# 4. String Indexing

Every character has an index.

Example

``` python
language = "PYTHON"
```

  Character        P    Y    T    H    O    N
  ---------------- ---- ---- ---- ---- ---- ----
  Positive Index   0    1    2    3    4    5
  Negative Index   -6   -5   -4   -3   -2   -1

------------------------------------------------------------------------

## Positive Index

``` python
language = "PYTHON"

print(language[0])
print(language[2])
print(language[5])
```

Output

    P
    T
    N

------------------------------------------------------------------------

## Negative Index

``` python
language = "PYTHON"

print(language[-1])
print(language[-2])
print(language[-6])
```

Output

    N
    O
    P

------------------------------------------------------------------------

# 5. String Slicing

### Syntax

``` python
string[start : stop : step]
```

-   start → Included
-   stop → Excluded
-   step → Optional

------------------------------------------------------------------------

## Forward Slicing

``` python
text = "PYTHON"

print(text[0:4])
print(text[2:6])
print(text[:4])
print(text[2:])
print(text[:])
```

Output

    PYTH
    THON
    PYTH
    THON
    PYTHON

------------------------------------------------------------------------

## Backward Slicing

``` python
text = "PYTHON"

print(text[::-1])
print(text[5:1:-1])
print(text[-1:-7:-1])
```

Output

    NOHTYP
    NOHT
    NOHTYP

------------------------------------------------------------------------

# 6. Behaviour of Slice Operator

## Moving Forward

``` python
text = "PYTHON"

print(text[1:5:1])
```

Output

    YTHO

------------------------------------------------------------------------

## Moving Backward

``` python
text = "PYTHON"

print(text[5:0:-1])
```

Output

    NOHTY

------------------------------------------------------------------------

## Empty Output Example

``` python
text = "PYTHON"

print(text[5:0])
```

Output

    ''

Reason: Forward movement is impossible because start \> stop.

------------------------------------------------------------------------

# 7. Mathematical Operations on Strings

## Addition (+)

Concatenation

``` python
first = "Hello"
second = "World"

print(first + " " + second)
```

Output

    Hello World

------------------------------------------------------------------------

## Multiplication (\*)

``` python
print("Python " * 3)
```

Output

    Python Python Python

------------------------------------------------------------------------

# 8. Built-in Function

## len()

Returns number of characters.

``` python
text = "Programming"

print(len(text))
```

Output

    11

------------------------------------------------------------------------

# 9. Membership Operators

## in

``` python
text = "Programming"

print("gram" in text)
```

Output

    True

------------------------------------------------------------------------

## not in

``` python
print("Java" not in text)
```

Output

    True

------------------------------------------------------------------------

# 10. String Comparisons

Strings are compared in **alphabetical (lexicographical)** order based
on Unicode values.

``` python
print("Apple" == "Apple")
print("Apple" != "apple")
print("Apple" < "Banana")
print("Cat" > "Ball")
print("abc" > "ABC")
```

Output

    True
    True
    True
    True
    True

------------------------------------------------------------------------

# 11. Popular String Methods

------------------------------------------------------------------------

## strip()

Removes spaces from both sides.

``` python
text = "   Python   "

print(text.strip())
```

Output

    Python

------------------------------------------------------------------------

## lstrip()

``` python
text = "   Python"

print(text.lstrip())
```

Output

    Python

------------------------------------------------------------------------

## rstrip()

``` python
text = "Python   "

print(text.rstrip())
```

Output

    Python

------------------------------------------------------------------------

## find()

Returns first occurrence.

``` python
text = "Programming"

print(text.find("gram"))
```

Output

    3

------------------------------------------------------------------------

## index()

``` python
text = "Programming"

print(text.index("gram"))
```

Output

    3

------------------------------------------------------------------------

## Difference

``` python
text = "Programming"

print(text.find("Java"))
```

Output

    -1

``` python
text.index("Java")
```

Output

    ValueError

------------------------------------------------------------------------

## count()

``` python
text = "banana"

print(text.count("a"))
```

Output

    3

------------------------------------------------------------------------

## replace()

``` python
text = "I like Java"

print(text.replace("Java","Python"))
```

Output

    I like Python

------------------------------------------------------------------------

## split()

``` python
text = "Python,Java,C++"

print(text.split(","))
```

Output

    ['Python', 'Java', 'C++']

------------------------------------------------------------------------

## join()

``` python
languages = ["Python","Java","C++"]

print(" - ".join(languages))
```

Output

    Python - Java - C++

------------------------------------------------------------------------

## lower()

``` python
text = "Python"

print(text.lower())
```

Output

    python

------------------------------------------------------------------------

## upper()

``` python
text = "Python"

print(text.upper())
```

Output

    PYTHON

------------------------------------------------------------------------

## swapcase()

``` python
text = "PyTHon"

print(text.swapcase())
```

Output

    pYthON

------------------------------------------------------------------------

## title()

``` python
text = "python programming language"

print(text.title())
```

Output

    Python Programming Language

------------------------------------------------------------------------

## capitalize()

``` python
text = "python programming"

print(text.capitalize())
```

Output

    Python programming

------------------------------------------------------------------------

## startswith()

``` python
text = "Python Programming"

print(text.startswith("Python"))
```

Output

    True

------------------------------------------------------------------------

## endswith()

``` python
text = "report.pdf"

print(text.endswith(".pdf"))
```

Output

    True

------------------------------------------------------------------------

## isalnum()

Letters and numbers only.

``` python
print("Python123".isalnum())
print("Python 123".isalnum())
```

Output

    True
    False

------------------------------------------------------------------------

## isalpha()

``` python
print("Python".isalpha())
print("Python123".isalpha())
```

Output

    True
    False

------------------------------------------------------------------------

## isdigit()

``` python
print("12345".isdigit())
print("12A45".isdigit())
```

Output

    True
    False

------------------------------------------------------------------------

## islower()

``` python
print("python".islower())
print("Python".islower())
```

Output

    True
    False

------------------------------------------------------------------------

## isupper()

``` python
print("PYTHON".isupper())
print("Python".isupper())
```

Output

    True
    False

------------------------------------------------------------------------

## istitle()

``` python
print("Python Programming".istitle())
print("python Programming".istitle())
```

Output

    True
    False

------------------------------------------------------------------------

## isspace()

``` python
print("   ".isspace())
print("Python".isspace())
```

Output

    True
    False

------------------------------------------------------------------------

# Quick Summary Table
------------------------------------------------------------------------

| Topic                                      | Key Concept                                                                      |
| ------------------------------------------ | -------------------------------------------------------------------------------- |
| String                                     | Sequence of characters enclosed in quotes                                        |
| type()                                     | Returns `<class 'str'>`                                                          |
| Triple Quotes                              | Multi-line strings                                                               |
| Positive Index                             | Left → Right (0,1,2...)                                                          |
| Negative Index                             | Right → Left (-1,-2...)                                                          |
| Slicing                                    | `string[start:stop:step]`                                                        |
| +                                          | Concatenate strings                                                              |
| *                                          | Repeat strings                                                                   |
| len()                                      | Length of string                                                                 |
| in / not in                                | Membership testing                                                               |
| Comparison                                 | Lexicographical (alphabetical/Unicode) order                                     |
| strip(), lstrip(), rstrip()                | Remove whitespace                                                                |
| find(), index()                            | Locate substring (`find()` returns `-1`; `index()` raises an error if not found) |
| count()                                    | Count occurrences                                                                |
| replace()                                  | Replace substring                                                                |
| split()                                    | Convert string to list                                                           |
| join()                                     | Join list into string                                                            |
| lower(), upper(), swapcase()               | Change case                                                                      |
| title(), capitalize()                      | Format text case                                                                 |
| startswith(), endswith()                   | Check prefix/suffix                                                              |
| isalnum(), isalpha(), isdigit()            | Character validation                                                             |
| islower(), isupper(), istitle(), isspace() | Case and whitespace checks                                                       |


# Self-Study Exercises

1.  Reverse a string using slicing.
2.  Count the number of vowels in a string.
3.  Check whether a string starts with `"https"`.
4.  Replace all spaces with underscores.
5.  Split a sentence into words.
6.  Join a list of names using commas.
7.  Count how many times `"Python"` appears in a sentence.
8.  Check whether a string is a palindrome.
9.  Convert a sentence to title case.
10. Remove leading and trailing spaces from user input.

------------------------------------------------------------------------

# 12. Practice Programs (Interview & Logic Building)

These programs strengthen your understanding of **string indexing,
slicing, loops, conditions, and string methods**.

## 1. Reverse a Given String (2 Methods)

### Method 1: Using Slicing

``` python
text = "PYTHON"
print(text[::-1])
```

### Method 2: Using Loop

``` python
text = "PYTHON"
reverse = ""
for ch in text:
    reverse = ch + reverse
print(reverse)
```

## 2. Print Characters at Even and Odd Positions (2 Methods)

### Method 1: Using Indexing

``` python
text = "PYTHON"

print("Even Position Characters")
for i in range(0, len(text), 2):
    print(text[i], end=" ")

print("\nOdd Position Characters")
for i in range(1, len(text), 2):
    print(text[i], end=" ")
```

### Method 2: Using Slicing

``` python
text = "PYTHON"

print("Even Position Characters :", text[::2])
print("Odd Position Characters  :", text[1::2])
```

## 3. Sort Characters First and Numbers Next

``` python
text = "B4A2D1C3"

chars = ""
nums = ""

for ch in text:
    if ch.isalpha():
        chars += ch
    elif ch.isdigit():
        nums += ch

chars = "".join(sorted(chars))
nums = "".join(sorted(nums))

print(chars + nums)
```

## 4. Expand Encoded String

``` python
text = "a4b3c5"

result = ""

for i in range(0, len(text), 2):
    result += text[i] * int(text[i+1])

print(result)
```

## 5. Remove Duplicate Characters

### Method 1

``` python
text = "programming"

result = ""

for ch in text:
    if ch not in result:
        result += ch

print(result)
```

### Method 2

``` python
text = "programming"

print("".join(dict.fromkeys(text)))
```
