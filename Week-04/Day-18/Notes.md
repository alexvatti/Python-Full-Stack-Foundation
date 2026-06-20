# Week-04 Day-18 — `re` Module & `string` Module
### Simple, Easy Guide with Examples & Exercises

---

## Table of Contents

1. [string Module](#1-string-module)
2. [re Module — Regular Expressions](#2-re-module--regular-expressions)
3. [Regex Special Characters (Quick Reference)](#3-regex-special-characters-quick-reference)
4. [re Module Functions](#4-re-module-functions)
5. [Practical Examples](#5-practical-examples)
6. [Self-Study Exercises — Level 1](#6-self-study-exercises--level-1)

---

## 1. `string` Module

The `string` module gives you ready-made **string constants** and a **Template** class. No need to type out the alphabet or digits yourself — just import and use.

```python
import string
```

### 1.1 String Constants

```python
import string

print(string.ascii_lowercase)   # abcdefghijklmnopqrstuvwxyz
print(string.ascii_uppercase)   # ABCDEFGHIJKLMNOPQRSTUVWXYZ
print(string.ascii_letters)     # abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
print(string.digits)            # 0123456789
print(string.hexdigits)         # 0123456789abcdefABCDEF
print(string.octdigits)         # 01234567
print(string.punctuation)       # !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
print(string.whitespace)        # space, tab, newline, etc.
print(string.printable)         # all printable characters combined
```

**Output:**
```
abcdefghijklmnopqrstuvwxyz
ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
0123456789
0123456789abcdefABCDEF
01234567
!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
```

### 1.2 Practical Uses of Constants

```python
import string

# Check if a password has digits
password = "Alex@123"
has_digit = any(ch in string.digits for ch in password)
print(has_digit)            # True

# Check if string has special characters
has_special = any(ch in string.punctuation for ch in password)
print(has_special)          # True

# Remove punctuation from a sentence
sentence = "Hello, World! How are you?"
clean = "".join(ch for ch in sentence if ch not in string.punctuation)
print(clean)                # Hello World How are you

# Count vowels
text = "Python Programming"
vowels = sum(1 for ch in text.lower() if ch in "aeiou")
print(vowels)               # 5

# Generate a simple random password
import random
chars = string.ascii_letters + string.digits + string.punctuation
password = "".join(random.choice(chars) for _ in range(10))
print(password)             # e.g. aX3@kL9!mQ
```

**Output:**
```
True
True
Hello World How are you
5
aX3@kL9!mQ  (random — varies each run)
```

### 1.3 `string.Template`

`Template` lets you substitute variables into a string using `$variable` placeholders.

```python
from string import Template

# Basic substitution
t = Template("Hello, $name! You scored $score marks.")
result = t.substitute(name="Alex", score=95)
print(result)           # Hello, Alex! You scored 95 marks.

# safe_substitute() — does NOT raise error for missing variables
t2 = Template("Dear $name, your order $order_id is ready.")
result2 = t2.safe_substitute(name="Bob")
print(result2)          # Dear Bob, your order $order_id is ready.

# Using a dictionary
data = {"city": "Hyderabad", "temp": 32}
t3 = Template("Today in $city the temperature is $temp°C.")
print(t3.substitute(data))
# Today in Hyderabad the temperature is 32°C.
```

**Output:**
```
Hello, Alex! You scored 95 marks.
Dear Bob, your order $order_id is ready.
Today in Hyderabad the temperature is 32°C.
```

---

## 2. `re` Module — Regular Expressions

The `re` module lets you **search, match, and manipulate strings using patterns**.

Think of a **regular expression (regex)** as a smart search — instead of looking for an exact word, you describe a *pattern* of characters.

```python
import re
```

### Why Use Regex?

| Task | Without Regex | With Regex |
|------|--------------|------------|
| Find email in text | Long manual code | One line |
| Validate phone number | Multiple if/else | One pattern |
| Replace all digits | Loop through chars | `re.sub()` |
| Split on multiple separators | Multiple `.split()` | One call |

### 2.1 Raw Strings — Always Use `r"..."` for Patterns

```python
# Without r prefix — \n means newline
print("\n")         # prints a blank line

# With r prefix — \n is treated as literal backslash-n
print(r"\n")        # prints \n

# Always write regex patterns as raw strings
pattern = r"\d+"    # matches one or more digits — CORRECT
pattern = "\\d+"    # same, but harder to read — AVOID
```

---

## 3. Regex Special Characters (Quick Reference)

### 3.1 Character Classes

| Pattern | Meaning | Example Match |
|---------|---------|---------------|
| `\d` | Any digit (0–9) | `"5"`, `"3"` |
| `\D` | Any non-digit | `"a"`, `"!"` |
| `\w` | Word character (a-z, A-Z, 0-9, _) | `"hello"`, `"x3"` |
| `\W` | Non-word character | `" "`, `","` |
| `\s` | Whitespace (space, tab, newline) | `" "`, `"\t"` |
| `\S` | Non-whitespace | `"a"`, `"5"` |
| `.` | Any character except newline | `"a"`, `"5"`, `"!"` |

```python
import re

text = "My phone is 9876543210 and pin is 500001"

print(re.findall(r"\d", text))    # ['9','8','7','6','5','4','3','2','1','0','5','0','0','0','0','1']
print(re.findall(r"\D", text))    # all non-digit characters
print(re.findall(r"\w+", text))   # ['My', 'phone', 'is', '9876543210', 'and', 'pin', 'is', '500001']
print(re.findall(r"\s", text))    # [' ', ' ', ' ', ' ', ' ', ' ']
```

### 3.2 Quantifiers — How Many Times?

| Pattern | Meaning |
|---------|---------|
| `*` | 0 or more times |
| `+` | 1 or more times |
| `?` | 0 or 1 time (optional) |
| `{n}` | Exactly n times |
| `{n,}` | n or more times |
| `{n,m}` | Between n and m times |

```python
import re

text = "colour color colouur"

print(re.findall(r"colou?r", text))       # ['colour', 'color']  — u is optional
print(re.findall(r"colou+r", text))       # ['colour', 'colouur'] — 1+ u's
print(re.findall(r"colou*r", text))       # ['colour', 'color', 'colouur'] — 0+ u's

# Digits
print(re.findall(r"\d{3}", "123 45 6789"))    # ['123', '678']  — exactly 3 digits
print(re.findall(r"\d{2,4}", "1 22 333 4444 55555"))  # ['22', '333', '4444', '5555']
```

### 3.3 Anchors — Position in String

| Pattern | Meaning |
|---------|---------|
| `^` | Start of string |
| `$` | End of string |
| `\b` | Word boundary |

```python
import re

# ^ start of string
print(re.findall(r"^\d+", "123 hello 456"))   # ['123']  — only at start
print(re.findall(r"^\d+", "hello 123"))       # []       — doesn't start with digit

# $ end of string
print(re.findall(r"\d+$", "hello 456"))       # ['456']
print(re.findall(r"\d+$", "456 hello"))       # []

# \b word boundary
print(re.findall(r"\bcat\b", "cat catfish concatenate"))  # ['cat']  — exact word only
```

### 3.4 Character Sets `[...]`

| Pattern | Meaning |
|---------|---------|
| `[aeiou]` | Any vowel |
| `[a-z]` | Any lowercase letter |
| `[A-Z]` | Any uppercase letter |
| `[0-9]` | Any digit (same as `\d`) |
| `[^aeiou]` | Any character that is NOT a vowel |
| `[a-zA-Z0-9]` | Any letter or digit |

```python
import re

text = "Hello World 123"

print(re.findall(r"[aeiouAEIOU]", text))    # ['e', 'o', 'o']  — vowels
print(re.findall(r"[^aeiouAEIOU\s]", text)) # consonants and digits
print(re.findall(r"[A-Z]", text))           # ['H', 'W']
print(re.findall(r"[a-z]+", text))          # ['ello', 'orld']
print(re.findall(r"[0-9]+", text))          # ['123']
```

### 3.5 Groups and Alternation

| Pattern | Meaning |
|---------|---------|
| `(abc)` | Group — captures `abc` |
| `a\|b` | a OR b |
| `(cat\|dog)` | either "cat" or "dog" |

```python
import re

# Alternation
text = "I have a cat and a dog and a fish"
print(re.findall(r"cat|dog", text))         # ['cat', 'dog']

# Groups — extract parts
date = "Today is 2024-06-20"
match = re.search(r"(\d{4})-(\d{2})-(\d{2})", date)
if match:
    print(match.group(0))   # 2024-06-20  (full match)
    print(match.group(1))   # 2024        (year)
    print(match.group(2))   # 06          (month)
    print(match.group(3))   # 20          (day)
```

**Output:**
```
['cat', 'dog']
2024-06-20
2024
06
20
```

---

## 4. `re` Module Functions

### 4.1 `re.search()` — Find First Match Anywhere

Returns a **match object** if pattern found anywhere in string, else `None`.

```python
import re

text = "My email is alex@gmail.com"

match = re.search(r"\w+@\w+\.\w+", text)
if match:
    print("Found:", match.group())      # Found: alex@gmail.com
    print("Start:", match.start())      # Start: 12
    print("End:",   match.end())        # End: 26
    print("Span:",  match.span())       # Span: (12, 26)
else:
    print("Not found")
```

### 4.2 `re.match()` — Match at the START Only

Only matches if pattern is at the **beginning** of the string.

```python
import re

# Matches — pattern is at start
m1 = re.match(r"\d+", "123 hello")
print(m1.group() if m1 else "No match")    # 123

# No match — pattern not at start
m2 = re.match(r"\d+", "hello 123")
print(m2.group() if m2 else "No match")    # No match

# Difference between match() and search()
text = "hello 123"
print(re.match(r"\d+", text))             # None   — not at start
print(re.search(r"\d+", text).group())    # 123    — found anywhere
```

### 4.3 `re.findall()` — Find ALL Matches

Returns a **list** of all non-overlapping matches.

```python
import re

text = "Prices: apple ₹50, banana ₹30, cherry ₹80"

# Find all numbers
numbers = re.findall(r"\d+", text)
print(numbers)              # ['50', '30', '80']

# Find all words
words = re.findall(r"[a-z]+", text)
print(words)                # ['rices', 'apple', 'banana', 'cherry']

# Find all words starting with vowel
text2 = "apple orange banana elderberry"
vowel_words = re.findall(r"\b[aeiou]\w*", text2)
print(vowel_words)          # ['apple', 'orange', 'elderberry']

# With groups — returns list of tuples
dates = "Start: 2024-01-15, End: 2024-06-20"
matches = re.findall(r"(\d{4})-(\d{2})-(\d{2})", dates)
print(matches)              # [('2024', '01', '15'), ('2024', '06', '20')]
```

### 4.4 `re.finditer()` — Find ALL Matches as Iterator

Like `findall()` but returns match objects one at a time — useful for large texts.

```python
import re

text = "Call 9876543210 or 8765432109 for support"

for match in re.finditer(r"\d{10}", text):
    print(f"Found: {match.group()} at position {match.start()}-{match.end()}")
```

**Output:**
```
Found: 9876543210 at position 5-15
Found: 8765432109 at position 19-29
```

### 4.5 `re.sub()` — Replace Matches

Replaces all occurrences of a pattern with a replacement string.

```python
import re

# Basic replacement
text = "My phone: 9876543210, backup: 8765432109"
masked = re.sub(r"\d{10}", "XXXXXXXXXX", text)
print(masked)       # My phone: XXXXXXXXXX, backup: XXXXXXXXXX

# Remove all punctuation
sentence = "Hello, World! How are you?"
clean = re.sub(r"[^\w\s]", "", sentence)
print(clean)        # Hello World How are you

# Replace multiple spaces with one
messy = "Hello    World   Python"
clean2 = re.sub(r"\s+", " ", messy)
print(clean2)       # Hello World Python

# Replace with count limit
text2 = "cat cat cat dog"
result = re.sub(r"cat", "rabbit", text2, count=2)
print(result)       # rabbit rabbit cat dog

# Using a function as replacement
def double_digit(m):
    return str(int(m.group()) * 2)

print(re.sub(r"\d+", double_digit, "price is 50 and qty is 3"))
# price is 100 and qty is 6
```

### 4.6 `re.split()` — Split by Pattern

Split a string using a regex pattern as the delimiter.

```python
import re

# Split on multiple separators
text = "one,two;three four|five"
parts = re.split(r"[,;| ]+", text)
print(parts)        # ['one', 'two', 'three', 'four', 'five']

# Split on whitespace
print(re.split(r"\s+", "hello   world   python"))
# ['hello', 'world', 'python']

# Split with max splits
print(re.split(r",", "a,b,c,d,e", maxsplit=2))
# ['a', 'b', 'c,d,e']
```

### 4.7 `re.compile()` — Pre-compile a Pattern

When you use the same pattern multiple times, compile it once for efficiency.

```python
import re

# Without compile — pattern compiled fresh every call
for text in ["alex@gmail.com", "bob@yahoo.com", "invalid-email"]:
    if re.search(r"\w+@\w+\.\w+", text):
        print(f"Valid: {text}")

# With compile — compile ONCE, use many times ✅
email_pattern = re.compile(r"\w+@\w+\.\w+")

for text in ["alex@gmail.com", "bob@yahoo.com", "invalid-email"]:
    if email_pattern.search(text):
        print(f"Valid: {text}")
    else:
        print(f"Invalid: {text}")
```

**Output:**
```
Valid: alex@gmail.com
Valid: bob@yahoo.com
Valid: alex@gmail.com
Valid: bob@yahoo.com
Invalid: invalid-email
```

### 4.8 Flags — Modify Matching Behaviour

| Flag | Short | Meaning |
|------|-------|---------|
| `re.IGNORECASE` | `re.I` | Case-insensitive match |
| `re.MULTILINE` | `re.M` | `^` and `$` match each line |
| `re.DOTALL` | `re.S` | `.` matches newline too |
| `re.VERBOSE` | `re.X` | Allow whitespace/comments in pattern |

```python
import re

# IGNORECASE
text = "Hello HELLO hello HeLLo"
print(re.findall(r"hello", text, re.I))     # ['Hello', 'HELLO', 'hello', 'HeLLo']

# MULTILINE — ^ matches start of each line
multi = "first line\nsecond line\nthird line"
print(re.findall(r"^\w+", multi, re.M))     # ['first', 'second', 'third']

# DOTALL — . matches newline
text2 = "start\nmiddle\nend"
print(re.search(r"start.*end", text2, re.S).group())
# start\nmiddle\nend

# VERBOSE — readable multi-line pattern
phone_pattern = re.compile(r"""
    \d{3}       # area code
    [-.\s]?     # optional separator
    \d{3}       # middle 3 digits
    [-.\s]?     # optional separator
    \d{4}       # last 4 digits
""", re.VERBOSE)

print(phone_pattern.findall("Call 987-654-3210 or 876.543.2109"))
# ['987-654-3210', '876.543.2109']
```

---

## 5. Practical Examples

### 5.1 Validate Email Address

```python
import re

def is_valid_email(email):
    pattern = r"^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z]{2,}$"
    return bool(re.match(pattern, email))

emails = ["alex@gmail.com", "bob.smith@company.co.in", "invalid@", "no-at-sign.com", "user@domain.org"]
for email in emails:
    status = "✅ Valid" if is_valid_email(email) else "❌ Invalid"
    print(f"  {status}: {email}")
```

**Output:**
```
  ✅ Valid: alex@gmail.com
  ✅ Valid: bob.smith@company.co.in
  ❌ Invalid: invalid@
  ❌ Invalid: no-at-sign.com
  ✅ Valid: user@domain.org
```

### 5.2 Validate Indian Mobile Number

```python
import re

def is_valid_mobile(number):
    pattern = r"^[6-9]\d{9}$"     # starts with 6-9, followed by 9 digits
    return bool(re.match(pattern, number))

numbers = ["9876543210", "8765432109", "1234567890", "98765", "6000000000"]
for num in numbers:
    status = "✅" if is_valid_mobile(num) else "❌"
    print(f"  {status} {num}")
```

**Output:**
```
  ✅ 9876543210
  ✅ 8765432109
  ❌ 1234567890
  ❌ 98765
  ✅ 6000000000
```

### 5.3 Extract All Emails from a Text

```python
import re

text = """
Contact us at support@company.com or sales@company.in
For billing: billing@company.org | Personal: john.doe@gmail.com
"""

emails = re.findall(r"[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z]{2,}", text)
print("Emails found:")
for email in emails:
    print(f"  {email}")
```

**Output:**
```
Emails found:
  support@company.com
  sales@company.in
  billing@company.org
  john.doe@gmail.com
```

### 5.4 Extract Dates from Text

```python
import re

text = "Invoice date: 15-06-2024, Due date: 30-06-2024, Payment: 01/07/2024"

# Match both - and / as separators
dates = re.findall(r"\d{2}[-/]\d{2}[-/]\d{4}", text)
print(dates)        # ['15-06-2024', '30-06-2024', '01/07/2024']
```

### 5.5 Password Strength Checker

```python
import re

def check_password(pwd):
    checks = {
        "At least 8 characters":     len(pwd) >= 8,
        "Has uppercase letter":       bool(re.search(r"[A-Z]", pwd)),
        "Has lowercase letter":       bool(re.search(r"[a-z]", pwd)),
        "Has digit":                  bool(re.search(r"\d", pwd)),
        "Has special character":      bool(re.search(r"[!@#$%^&*]", pwd)),
    }
    for check, result in checks.items():
        icon = "✅" if result else "❌"
        print(f"  {icon} {check}")
    strength = sum(checks.values())
    print(f"  Strength: {strength}/5")

print("Password: Alex@123")
check_password("Alex@123")
print("\nPassword: hello")
check_password("hello")
```

**Output:**
```
Password: Alex@123
  ✅ At least 8 characters
  ✅ Has uppercase letter
  ✅ Has lowercase letter
  ✅ Has digit
  ✅ Has special character
  Strength: 5/5

Password: hello
  ❌ At least 8 characters
  ❌ Has uppercase letter
  ✅ Has lowercase letter
  ❌ Has digit
  ❌ Has special character
  Strength: 1/5
```

---

## 6. Self-Study Exercises — Level 1

### `string` Module Exercises

**Exercise 1**
Import the `string` module and print all lowercase letters, uppercase letters, and digits on separate lines.

```python
# Expected Output:
# abcdefghijklmnopqrstuvwxyz
# ABCDEFGHIJKLMNOPQRSTUVWXYZ
# 0123456789
```

**Exercise 2**
Write a program that takes the string `"Hello, World! 123"` and removes all punctuation characters using `string.punctuation`.

```python
# Expected Output: Hello World 123
```

**Exercise 3**
Use `string.Template` to create a simple invoice message:
`"Dear [name], your invoice of ₹[amount] is due on [date]."`
Substitute with: name = "Alex", amount = 5000, date = "30-June-2024".

```python
# Expected Output: Dear Alex, your invoice of ₹5000 is due on 30-June-2024.
```

**Exercise 4**
Write a program to count how many digits, letters, and special characters are in the string `"Alex@2024!"` using `string` constants.

```python
# Expected Output:
# Digits: 4
# Letters: 4
# Special: 2
```

**Exercise 5**
Generate a random 8-character password using `string.ascii_letters` and `string.digits`.

```python
import random, string
# Hint: use random.choice() in a loop or random.choices()
# Sample Output: kT3mX9aQ
```

---

### `re` Module Exercises

**Exercise 6**
Use `re.findall()` to extract all numbers from the string:
`"I have 3 cats, 2 dogs, and 10 fish."`

```python
# Expected Output: ['3', '2', '10']
```

**Exercise 7**
Write a program using `re.search()` to check if the word `"Python"` exists in the sentence `"I love Python programming"`. Print `"Found"` or `"Not Found"`.

```python
# Expected Output: Found
```

**Exercise 8**
Use `re.sub()` to replace all spaces in `"Hello World Python"` with underscores `_`.

```python
# Expected Output: Hello_World_Python
```

**Exercise 9**
Use `re.split()` to split `"one,two;three four"` into a list using commas, semicolons, and spaces as separators.

```python
# Expected Output: ['one', 'two', 'three', 'four']
```

**Exercise 10**
Write a program to check if a string starts with a digit using `re.match()`. Test with `"123abc"` and `"abc123"`.

```python
# Expected Output:
# 123abc → Starts with digit
# abc123 → Does not start with digit
```

**Exercise 11**
Use `re.findall()` to find all words in `"cat bat hat rat sat"` that end with `"at"`.

```python
# Expected Output: ['cat', 'bat', 'hat', 'rat', 'sat']
```

**Exercise 12**
Write a program using `re.findall()` to extract all email addresses from:
`"Send to alice@gmail.com and bob@yahoo.in for details"`

```python
# Expected Output: ['alice@gmail.com', 'bob@yahoo.in']
```

**Exercise 13**
Use `re.sub()` to remove all digits from `"h3ll0 w0rld py7h0n"` and print the result.

```python
# Expected Output: hll wrld pyhn
```

**Exercise 14**
Write a program using `re.findall()` with `re.IGNORECASE` flag to find all occurrences of `"python"` in:
`"Python is great. I love PYTHON. python rocks!"`

```python
# Expected Output: ['Python', 'PYTHON', 'python']
```

**Exercise 15**
Compile a regex pattern to match a 6-digit PIN code. Test it against `"500001"`, `"12345"`, `"abcdef"`, and `"500001x"`.

```python
# Expected Output:
# 500001  → Valid PIN
# 12345   → Invalid PIN
# abcdef  → Invalid PIN
# 500001x → Invalid PIN
```

---

## Quick Cheat Sheet

### `string` Module

```python
import string
string.ascii_lowercase    # a-z
string.ascii_uppercase    # A-Z
string.ascii_letters      # a-z + A-Z
string.digits             # 0-9
string.punctuation        # all special chars
string.Template("Hi $name").substitute(name="Alex")
```

### `re` Module

```python
import re
re.search(pattern, text)          # first match anywhere → match object or None
re.match(pattern, text)           # match at START only → match object or None
re.findall(pattern, text)         # all matches → list
re.finditer(pattern, text)        # all matches → iterator of match objects
re.sub(pattern, replace, text)    # replace matches → new string
re.split(pattern, text)           # split by pattern → list
re.compile(pattern)               # pre-compile pattern → pattern object

# Common patterns
r"\d+"        # one or more digits
r"\w+"        # one or more word characters
r"\s+"        # one or more whitespace
r"[A-Z]"      # any uppercase letter
r"^..."       # starts with
r"...$"       # ends with
r"(a|b)"      # a or b
```

---

*End of Week-04 Day-18 — `re` Module & `string` Module*
