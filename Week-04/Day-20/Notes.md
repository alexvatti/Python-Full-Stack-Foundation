# Week-04 Day-20 — `json` Module
### Simple & Easy Guide — Read, Write, Convert JSON in Python

---

## Table of Contents

1. [What is JSON?](#1-what-is-json)
2. [JSON vs Python — Data Type Mapping](#2-json-vs-python--data-type-mapping)
3. [The 4 Core Functions](#3-the-4-core-functions)
4. [json.dumps() — Python → JSON String](#4-jsondumps--python--json-string)
5. [json.loads() — JSON String → Python](#5-jsonloads--json-string--python)
6. [json.dump() — Python → JSON File](#6-jsondump--python--json-file)
7. [json.load() — JSON File → Python](#7-jsonload--json-file--python)
8. [Pretty Printing JSON](#8-pretty-printing-json)
9. [Handling Nested JSON](#9-handling-nested-json)
10. [JSON with the requests Module](#10-json-with-the-requests-module)
11. [Error Handling](#11-error-handling)
12. [Real-World Examples](#12-real-world-examples)
13. [Self-Study Exercises — Level 1](#13-self-study-exercises--level-1)
14. [Quick Cheat Sheet](#14-quick-cheat-sheet)

---

## 1. What is JSON?

**JSON** stands for **JavaScript Object Notation**. It is a lightweight, human-readable format for storing and exchanging data between systems — between Python and a web API, between a server and a database, or between two programs.

```json
{
  "name": "Alex",
  "age": 25,
  "city": "Hyderabad",
  "scores": [95, 88, 92],
  "active": true,
  "address": null
}
```

### Where You See JSON Every Day

| Situation | JSON is used for |
|-----------|-----------------|
| Calling an API | The response comes back as JSON |
| Config files | `settings.json`, `package.json` |
| Saving app data | Storing user profiles, preferences |
| Sending data to a server | POST body is usually JSON |
| Database exports | MongoDB, Firebase export as JSON |

### Import the Module

```python
import json    # built-in — no pip install needed
```

---

## 2. JSON vs Python — Data Type Mapping

When you convert between Python and JSON, the types map like this:

| Python | JSON | Example |
|--------|------|---------|
| `dict` | `object` | `{"name": "Alex"}` |
| `list` | `array` | `[1, 2, 3]` |
| `tuple` | `array` | `(1, 2, 3)` → `[1, 2, 3]` |
| `str` | `string` | `"hello"` |
| `int` | `number` | `42` |
| `float` | `number` | `3.14` |
| `True` | `true` | `true` |
| `False` | `false` | `false` |
| `None` | `null` | `null` |

> **Important:** JSON uses lowercase `true`, `false`, `null` — Python uses `True`, `False`, `None`.
> Tuples become arrays in JSON and come back as lists when loaded.

```python
import json

# Python → JSON conversion demo
python_data = {
    "name":   "Alex",
    "age":    25,
    "scores": [95, 88, 92],
    "passed": True,
    "grade":  None,
    "ratio":  3.14
}

json_string = json.dumps(python_data)
print(json_string)
# {"name": "Alex", "age": 25, "scores": [95, 88, 92], "passed": true, "grade": null, "ratio": 3.14}
#                                                                        ^^^^           ^^^^
#                                                                 True→true         None→null
```

---

## 3. The 4 Core Functions

These are the only 4 functions you need to know:

| Function | Direction | Works with |
|----------|-----------|------------|
| `json.dumps()` | Python → JSON string | memory (variable) |
| `json.loads()` | JSON string → Python | memory (variable) |
| `json.dump()` | Python → JSON file | file on disk |
| `json.load()` | JSON file → Python | file on disk |

### Easy Memory Trick

```
dumps / loads  →  "s" = string   →  works with strings in memory
dump  / load   →  no "s"         →  works with files on disk
```

```
Python dict  ──dumps()──▶  JSON string
Python dict  ◀──loads()──  JSON string

Python dict  ──dump()───▶  JSON file
Python dict  ◀──load()───  JSON file
```

---

## 4. `json.dumps()` — Python → JSON String

`dumps` = **dump string** — converts a Python object into a JSON-formatted **string**.

```python
import json

# Dict → JSON string
student = {
    "name":   "Alex",
    "age":    25,
    "city":   "Hyderabad",
    "passed": True,
    "score":  None
}

json_str = json.dumps(student)
print(json_str)
print(type(json_str))   # <class 'str'>
```

**Output:**
```
{"name": "Alex", "age": 25, "city": "Hyderabad", "passed": true, "score": null}
<class 'str'>
```

### dumps() with Options

```python
import json

data = {"name": "Alex", "age": 25, "city": "Hyderabad"}

# indent — pretty print with spaces
print(json.dumps(data, indent=4))

# sort_keys — alphabetical order
print(json.dumps(data, sort_keys=True))

# separators — compact format (no spaces)
print(json.dumps(data, separators=(",", ":")))
```

**Output:**
```json
{
    "name": "Alex",
    "age": 25,
    "city": "Hyderabad"
}

{"age": 25, "city": "Hyderabad", "name": "Alex"}

{"name":"Alex","age":25,"city":"Hyderabad"}
```

### dumps() with List and Tuple

```python
import json

# List → JSON array
scores = [95, 88, 92, 78]
print(json.dumps(scores))        # [95, 88, 92, 78]

# Tuple → also becomes JSON array
coords = (17.38, 78.47)
print(json.dumps(coords))        # [17.38, 78.47]

# Nested structure
payload = {
    "user":   "Alex",
    "tags":   ["python", "api", "json"],
    "meta":   {"version": 1, "active": True}
}
print(json.dumps(payload, indent=2))
```

**Output:**
```json
[95, 88, 92, 78]
[17.38, 78.47]
{
  "user": "Alex",
  "tags": [
    "python",
    "api",
    "json"
  ],
  "meta": {
    "version": 1,
    "active": true
  }
}
```

---

## 5. `json.loads()` — JSON String → Python

`loads` = **load string** — converts a JSON **string** back into a Python object.

```python
import json

# JSON string (what an API sends you)
json_str = '{"name": "Alex", "age": 25, "city": "Hyderabad", "passed": true, "score": null}'

# Convert to Python dict
data = json.loads(json_str)

print(data)
print(type(data))           # <class 'dict'>

# Now you can access it like a normal dict
print(data["name"])         # Alex
print(data["passed"])       # True   (JSON true → Python True)
print(data["score"])        # None   (JSON null → Python None)
print(data.get("age"))      # 25
```

**Output:**
```
{'name': 'Alex', 'age': 25, 'city': 'Hyderabad', 'passed': True, 'score': None}
<class 'dict'>
Alex
True
None
25
```

### loads() with JSON Array

```python
import json

# JSON array string
json_array = '[{"id": 1, "name": "Alice"}, {"id": 2, "name": "Bob"}]'

users = json.loads(json_array)
print(type(users))          # <class 'list'>
print(len(users))           # 2

for user in users:
    print(f"  {user['id']}: {user['name']}")
```

**Output:**
```
<class 'list'>
2
  1: Alice
  2: Bob
```

### Round-Trip: Python → JSON string → Python

```python
import json

original = {"name": "Alex", "scores": [95, 88], "active": True}

# Encode (Python → JSON string)
encoded = json.dumps(original)
print(f"Encoded : {encoded}")
print(f"Type    : {type(encoded)}")

# Decode (JSON string → Python)
decoded = json.loads(encoded)
print(f"Decoded : {decoded}")
print(f"Type    : {type(decoded)}")

# They are equal
print(f"Equal   : {original == decoded}")
```

**Output:**
```
Encoded : {"name": "Alex", "scores": [95, 88], "active": true}
Type    : <class 'str'>
Decoded : {'name': 'Alex', 'scores': [95, 88], 'active': True}
Type    : <class 'dict'>
Equal   : True
```

---

## 6. `json.dump()` — Python → JSON File

`dump` (no s) — writes a Python object **directly to a file** on disk.

```python
import json

student = {
    "name":    "Alex",
    "age":     25,
    "city":    "Hyderabad",
    "courses": ["Python", "SQL", "ML"],
    "active":  True
}

# Write to file
with open("student.json", "w") as file:
    json.dump(student, file, indent=4)

print("File saved successfully!")
```

**File saved — `student.json` contents:**
```json
{
    "name": "Alex",
    "age": 25,
    "city": "Hyderabad",
    "courses": [
        "Python",
        "SQL",
        "ML"
    ],
    "active": true
}
```

### dump() a List of Records

```python
import json

employees = [
    {"id": 1, "name": "Alice", "dept": "Engineering", "salary": 85000},
    {"id": 2, "name": "Bob",   "dept": "Marketing",   "salary": 65000},
    {"id": 3, "name": "Charlie","dept": "Engineering", "salary": 95000}
]

with open("employees.json", "w") as file:
    json.dump(employees, file, indent=2)

print(f"Saved {len(employees)} employees to employees.json")
```

**`employees.json`:**
```json
[
  {"id": 1, "name": "Alice",   "dept": "Engineering", "salary": 85000},
  {"id": 2, "name": "Bob",     "dept": "Marketing",   "salary": 65000},
  {"id": 3, "name": "Charlie", "dept": "Engineering", "salary": 95000}
]
```

---

## 7. `json.load()` — JSON File → Python

`load` (no s) — reads a JSON file from disk and returns a Python object.

```python
import json

# Read the file we saved earlier
with open("student.json", "r") as file:
    student = json.load(file)

print(type(student))            # <class 'dict'>
print(student["name"])          # Alex
print(student["courses"])       # ['Python', 'SQL', 'ML']
print(student["active"])        # True
```

**Output:**
```
<class 'dict'>
Alex
['Python', 'SQL', 'ML']
True
```

### load() a List File

```python
import json

with open("employees.json", "r") as file:
    employees = json.load(file)

print(f"Loaded {len(employees)} employees")

for emp in employees:
    print(f"  [{emp['id']}] {emp['name']} — {emp['dept']} — ₹{emp['salary']:,}")
```

**Output:**
```
Loaded 3 employees
  [1] Alice — Engineering — ₹85,000
  [2] Bob — Marketing — ₹65,000
  [3] Charlie — Engineering — ₹95,000
```

### Update a JSON File (Read → Modify → Write)

```python
import json

# Read
with open("student.json", "r") as f:
    student = json.load(f)

# Modify
student["age"] = 26
student["courses"].append("Deep Learning")
student["city"] = "Chennai"

# Write back
with open("student.json", "w") as f:
    json.dump(student, f, indent=4)

print("File updated!")

# Verify
with open("student.json", "r") as f:
    updated = json.load(f)
print(updated)
```

**Output:**
```
File updated!
{'name': 'Alex', 'age': 26, 'city': 'Chennai',
 'courses': ['Python', 'SQL', 'ML', 'Deep Learning'], 'active': True}
```

---

## 8. Pretty Printing JSON

Use `indent`, `sort_keys`, and `separators` to control how JSON looks.

```python
import json

data = {
    "name": "Alex",
    "skills": ["Python", "SQL", "ML"],
    "address": {"city": "Hyderabad", "pin": 500001},
    "active": True
}

# Default — compact, hard to read
print("Default:")
print(json.dumps(data))

print()

# indent=4 — readable, 4-space indent
print("indent=4:")
print(json.dumps(data, indent=4))

print()

# indent=2 + sort_keys — sorted alphabetically
print("indent=2, sort_keys=True:")
print(json.dumps(data, indent=2, sort_keys=True))

print()

# Compact — smallest possible output
print("Compact (separators):")
print(json.dumps(data, separators=(",", ":")))
```

**Output:**
```
Default:
{"name": "Alex", "skills": ["Python", "SQL", "ML"], "address": {"city": "Hyderabad", "pin": 500001}, "active": true}

indent=4:
{
    "name": "Alex",
    "skills": [
        "Python",
        "SQL",
        "ML"
    ],
    "address": {
        "city": "Hyderabad",
        "pin": 500001
    },
    "active": true
}

indent=2, sort_keys=True:
{
  "active": true,
  "address": {
    "city": "Hyderabad",
    "pin": 500001
  },
  "name": "Alex",
  "skills": [
    "Python",
    "SQL",
    "ML"
  ]
}

Compact (separators):
{"name":"Alex","skills":["Python","SQL","ML"],"address":{"city":"Hyderabad","pin":500001},"active":true}
```

### Print any JSON beautifully with one line

```python
import json

# Any dict or list — instant pretty print
def pprint_json(data):
    print(json.dumps(data, indent=4, sort_keys=True))

pprint_json({"z": 3, "a": 1, "m": 2})
```

**Output:**
```json
{
    "a": 1,
    "m": 2,
    "z": 3
}
```

---

## 9. Handling Nested JSON

Real API responses are deeply nested. Here's how to navigate them.

```python
import json

# A typical API response
api_response = """
{
    "status": "success",
    "data": {
        "user": {
            "id": 101,
            "name": "Alex",
            "contact": {
                "email": "alex@example.com",
                "phone": "9876543210"
            },
            "orders": [
                {"id": "ORD001", "item": "Laptop",  "amount": 75000, "paid": true},
                {"id": "ORD002", "item": "Mouse",   "amount": 1500,  "paid": false},
                {"id": "ORD003", "item": "Monitor", "amount": 18000, "paid": true}
            ]
        }
    },
    "total_orders": 3
}
"""

# Parse the JSON string
data = json.loads(api_response)

# Navigate the structure step by step
user   = data["data"]["user"]
orders = user["orders"]

print(f"User    : {user['name']}")
print(f"Email   : {user['contact']['email']}")
print(f"Phone   : {user['contact']['phone']}")
print(f"Orders  : {data['total_orders']}")
print()

# Loop through orders
total_paid = 0
for order in orders:
    status = "✅ Paid" if order["paid"] else "⏳ Pending"
    print(f"  {order['id']}  {order['item']:<10}  ₹{order['amount']:>7,}  {status}")
    if order["paid"]:
        total_paid += order["amount"]

print(f"\nTotal Paid: ₹{total_paid:,}")

# Safe access with .get() — no crash if key missing
rating = data.get("rating", "Not rated")
print(f"Rating: {rating}")
```

**Output:**
```
User    : Alex
Email   : alex@example.com
Phone   : 9876543210
Orders  : 3

  ORD001  Laptop      ₹ 75,000  ✅ Paid
  ORD002  Mouse       ₹  1,500  ⏳ Pending
  ORD003  Monitor     ₹ 18,000  ✅ Paid

Total Paid: ₹93,000
Rating: Not rated
```

### Extract Specific Fields from a List of JSON Objects

```python
import json

# List of user records (from an API)
raw = """
[
    {"id": 1, "name": "Alice",   "age": 28, "dept": "Engineering", "salary": 85000},
    {"id": 2, "name": "Bob",     "age": 32, "dept": "Marketing",   "salary": 65000},
    {"id": 3, "name": "Charlie", "age": 29, "dept": "Engineering", "salary": 95000},
    {"id": 4, "name": "Diana",   "age": 26, "dept": "HR",          "salary": 55000}
]
"""

users = json.loads(raw)

# Extract only name and salary
print("Name & Salary:")
for u in users:
    print(f"  {u['name']:<10} ₹{u['salary']:,}")

# Filter — Engineering only
print("\nEngineering team:")
eng = [u for u in users if u["dept"] == "Engineering"]
for u in eng:
    print(f"  {u['name']}")

# Find highest salary
top = max(users, key=lambda u: u["salary"])
print(f"\nHighest paid: {top['name']} — ₹{top['salary']:,}")
```

**Output:**
```
Name & Salary:
  Alice      ₹85,000
  Bob        ₹65,000
  Charlie    ₹95,000
  Diana      ₹55,000

Engineering team:
  Alice
  Charlie

Highest paid: Charlie — ₹95,000
```

---

## 10. JSON with the `requests` Module

The most common real-world use — API responses come as JSON.

```python
import requests
import json

# ── Method 1: response.json() ── easiest, most common
response = requests.get("https://jsonplaceholder.typicode.com/users/1")
user = response.json()          # requests parses JSON automatically
print(user["name"])             # Leanne Graham


# ── Method 2: json.loads(response.text) ── manual parse
response2 = requests.get("https://jsonplaceholder.typicode.com/users/2")
user2 = json.loads(response2.text)
print(user2["name"])            # Ervin Howell


# ── Sending JSON in POST body ──────────────────────────────
new_post = {"title": "Hello JSON", "body": "Testing POST", "userId": 1}

# Option A: json= parameter (sets Content-Type automatically)
r = requests.post(
    "https://jsonplaceholder.typicode.com/posts",
    json=new_post
)
print(r.json())     # {'title': 'Hello JSON', ..., 'id': 101}


# Option B: manually convert and set header
r2 = requests.post(
    "https://jsonplaceholder.typicode.com/posts",
    data=json.dumps(new_post),
    headers={"Content-Type": "application/json"}
)
print(r2.json())    # same result


# ── Save API response to file ──────────────────────────────
response3 = requests.get("https://jsonplaceholder.typicode.com/users")
users = response3.json()

with open("users_from_api.json", "w") as f:
    json.dump(users, f, indent=2)

print(f"Saved {len(users)} users to users_from_api.json")
```

**Output:**
```
Leanne Graham
Ervin Howell
{'title': 'Hello JSON', 'body': 'Testing POST', 'userId': 1, 'id': 101}
{'title': 'Hello JSON', 'body': 'Testing POST', 'userId': 1, 'id': 101}
Saved 10 users to users_from_api.json
```

---

## 11. Error Handling

### JSONDecodeError — Invalid JSON String

```python
import json

# Valid JSON
good = '{"name": "Alex", "age": 25}'
print(json.loads(good))             # {'name': 'Alex', 'age': 25}

# Invalid JSON — single quotes instead of double quotes
bad = "{'name': 'Alex'}"
try:
    json.loads(bad)
except json.JSONDecodeError as e:
    print(f"❌ JSONDecodeError: {e}")

# Invalid JSON — trailing comma
bad2 = '{"name": "Alex", "age": 25,}'
try:
    json.loads(bad2)
except json.JSONDecodeError as e:
    print(f"❌ JSONDecodeError: {e}")

# Invalid JSON — unquoted key
bad3 = '{name: "Alex"}'
try:
    json.loads(bad3)
except json.JSONDecodeError as e:
    print(f"❌ JSONDecodeError: {e}")
```

**Output:**
```
{'name': 'Alex', 'age': 25}
❌ JSONDecodeError: Expecting property name enclosed in double quotes: line 1 column 2 (char 1)
❌ JSONDecodeError: Expecting property name enclosed in double quotes: line 1 column 28 (char 27)
❌ JSONDecodeError: Expecting property name enclosed in double quotes: line 1 column 2 (char 1)
```

### TypeError — Non-Serialisable Types

```python
import json
from datetime import datetime

# datetime is NOT JSON serialisable by default
data = {"name": "Alex", "created_at": datetime.now()}
try:
    json.dumps(data)
except TypeError as e:
    print(f"❌ TypeError: {e}")

# Fix 1 — convert to string before dumping
data["created_at"] = str(datetime.now())
print(json.dumps(data, indent=2))

# Fix 2 — use default parameter with a converter function
def convert(obj):
    if isinstance(obj, datetime):
        return obj.isoformat()
    raise TypeError(f"Type {type(obj)} not serialisable")

data2 = {"name": "Alex", "created_at": datetime.now()}
print(json.dumps(data2, default=convert, indent=2))
```

**Output:**
```
❌ TypeError: Object of type datetime is not JSON serializable

{
  "name": "Alex",
  "created_at": "2024-06-20 14:32:11.123456"
}

{
  "name": "Alex",
  "created_at": "2024-06-20T14:32:11.123456"
}
```

### File Not Found

```python
import json

try:
    with open("missing_file.json", "r") as f:
        data = json.load(f)
except FileNotFoundError:
    print("❌ File not found — check the filename or path")
except json.JSONDecodeError as e:
    print(f"❌ File exists but contains invalid JSON: {e}")
```

**Output:**
```
❌ File not found — check the filename or path
```

---

## 12. Real-World Examples

### Example 1: Save & Load a Config File

```python
import json
import os

CONFIG_FILE = "config.json"

def save_config(config):
    with open(CONFIG_FILE, "w") as f:
        json.dump(config, f, indent=4)
    print("✅ Config saved")

def load_config():
    if not os.path.exists(CONFIG_FILE):
        print("⚠️  No config file found — using defaults")
        return {"theme": "light", "language": "en", "notifications": True}
    with open(CONFIG_FILE, "r") as f:
        return json.load(f)

# First run — save a config
config = {
    "theme":         "dark",
    "language":      "en",
    "font_size":     14,
    "notifications": True,
    "last_user":     "alex@example.com"
}
save_config(config)

# Later — load and use it
loaded = load_config()
print(f"Theme    : {loaded['theme']}")
print(f"Font     : {loaded['font_size']}")
print(f"Language : {loaded['language']}")
```

**Output:**
```
✅ Config saved
Theme    : dark
Font     : 14
Language : en
```

---

### Example 2: Student Score Tracker

```python
import json
import os

FILE = "scores.json"

def load_scores():
    if os.path.exists(FILE):
        with open(FILE, "r") as f:
            return json.load(f)
    return {}

def save_scores(scores):
    with open(FILE, "w") as f:
        json.dump(scores, f, indent=4)

def add_score(name, subject, score):
    scores = load_scores()
    if name not in scores:
        scores[name] = {}
    scores[name][subject] = score
    save_scores(scores)
    print(f"✅ Saved: {name} → {subject}: {score}")

def show_report():
    scores = load_scores()
    print("\n📊 Score Report")
    print("-" * 40)
    for name, subjects in scores.items():
        avg = sum(subjects.values()) / len(subjects)
        print(f"  {name:<12} Avg: {avg:.1f}")
        for subject, score in subjects.items():
            print(f"    {subject:<12}: {score}")

# Add scores
add_score("Alice",   "Math",    92)
add_score("Alice",   "Science", 88)
add_score("Bob",     "Math",    75)
add_score("Bob",     "Science", 80)
add_score("Charlie", "Math",    95)
add_score("Charlie", "Science", 91)

# Show report
show_report()
```

**Output:**
```
✅ Saved: Alice → Math: 92
✅ Saved: Alice → Science: 88
✅ Saved: Bob → Math: 75
✅ Saved: Bob → Science: 80
✅ Saved: Charlie → Math: 95
✅ Saved: Charlie → Science: 91

📊 Score Report
----------------------------------------
  Alice        Avg: 90.0
    Math        : 92
    Science     : 88
  Bob          Avg: 77.5
    Math        : 75
    Science     : 80
  Charlie      Avg: 93.0
    Math        : 95
    Science     : 91
```

---

### Example 3: Parse a Real API Response & Save to File

```python
import requests
import json

# Fetch users from a free API
url = "https://jsonplaceholder.typicode.com/users"
response = requests.get(url)
users = response.json()

# Extract only the fields we need
clean_users = []
for user in users:
    clean_users.append({
        "id":      user["id"],
        "name":    user["name"],
        "email":   user["email"],
        "city":    user["address"]["city"],
        "company": user["company"]["name"]
    })

# Save cleaned data to file
with open("clean_users.json", "w") as f:
    json.dump(clean_users, f, indent=2)

print(f"✅ Saved {len(clean_users)} users to clean_users.json\n")

# Print a summary
for u in clean_users[:4]:
    print(f"  [{u['id']}] {u['name']:<20} {u['email']}")
```

**Output:**
```
✅ Saved 10 users to clean_users.json

  [1] Leanne Graham        Sincere@april.biz
  [2] Ervin Howell         Shanna@melissa.tv
  [3] Clementine Bauch     Nathan@yesenia.net
  [4] Patricia Lebsack     Julianne.OConner@kory.org
```

---

## 13. Self-Study Exercises — Level 1

**Exercise 1 — dumps() basics**
Create a Python dictionary for a product:
- `name`, `price`, `in_stock` (True), `tags` (list of 3 strings)

Convert it to a JSON string using `json.dumps()` with `indent=4`.
Print the result and verify `True` becomes `true` in the output.

```python
# Expected Output:
# {
#     "name": "Laptop",
#     "price": 75000,
#     "in_stock": true,
#     "tags": ["electronics", "computers", "sale"]
# }
```

---

**Exercise 2 — loads() basics**
You receive this JSON string from an API:

```python
json_str = '{"country": "India", "capital": "New Delhi", "population": 1380004385, "member_un": true}'
```

Parse it using `json.loads()` and print:
- The country name
- The capital
- Population formatted with commas (e.g. `1,380,004,385`)
- Whether it is a UN member

```python
# Expected Output:
# Country    : India
# Capital    : New Delhi
# Population : 1,380,004,385
# UN Member  : True
```

---

**Exercise 3 — dump() to file**
Create a list of 3 students (each with `name`, `age`, `grade`) and save it to a file called `students.json` using `json.dump()` with `indent=4`.
Then open the file and print its contents to verify it was saved correctly.

```python
# students.json should look like:
# [
#     {"name": "Alice", "age": 20, "grade": "A"},
#     ...
# ]
```

---

**Exercise 4 — load() from file**
Load the `students.json` file you created in Exercise 3.
Loop through the students and print each one in this format:
`Alice (Age: 20) → Grade: A`

---

**Exercise 5 — Error Handling**
Write a function `safe_parse(text)` that:
- Tries to parse the given string as JSON
- Returns the parsed data if successful
- Prints `"Invalid JSON: <error message>"` and returns `None` if it fails

Test it with one valid and one invalid JSON string.

```python
safe_parse('{"name": "Alex"}')       # should work
safe_parse("{'name': 'Alex'}")       # should print error

# Expected Output:
# Parsed: {'name': 'Alex'}
# Invalid JSON: Expecting property name enclosed in double quotes...
```

---

## 14. Quick Cheat Sheet

```python
import json

# ── 4 CORE FUNCTIONS ──────────────────────────────────────────

json.dumps(data)                  # Python  → JSON string
json.loads(json_str)              # JSON string → Python

json.dump(data, file_obj)         # Python  → JSON file
json.load(file_obj)               # JSON file  → Python

# ── dumps() OPTIONS ───────────────────────────────────────────

json.dumps(data, indent=4)               # pretty print
json.dumps(data, sort_keys=True)         # sort alphabetically
json.dumps(data, separators=(",", ":"))  # compact, no spaces
json.dumps(data, indent=2, sort_keys=True)  # both

# ── WRITE TO FILE ─────────────────────────────────────────────

with open("data.json", "w") as f:
    json.dump(data, f, indent=4)

# ── READ FROM FILE ────────────────────────────────────────────

with open("data.json", "r") as f:
    data = json.load(f)

# ── WITH requests ─────────────────────────────────────────────

import requests
r = requests.get(url)
data = r.json()                    # parse response JSON
r2 = requests.post(url, json=payload)  # send JSON body

# ── ERROR HANDLING ────────────────────────────────────────────

try:
    data = json.loads(text)
except json.JSONDecodeError as e:
    print(f"Invalid JSON: {e}")

try:
    with open("file.json") as f:
        data = json.load(f)
except FileNotFoundError:
    print("File not found")
except json.JSONDecodeError as e:
    print(f"Bad JSON in file: {e}")

# ── TYPE MAPPING ──────────────────────────────────────────────

# Python    →  JSON        Python    ←  JSON
# dict      →  object      dict      ←  object
# list      →  array       list      ←  array
# tuple     →  array       list      ←  array  (tuples come back as lists!)
# str       →  string      str       ←  string
# int/float →  number      int/float ←  number
# True      →  true        True      ←  true
# False     →  false       False     ←  false
# None      →  null        None      ←  null
```

---

*End of Week-04 Day-20 — `json` Module*
