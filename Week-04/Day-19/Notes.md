# Week-04 Day-19 — `requests` Module
### Calling Real Web APIs with Python — Simple & Easy

> **APIs used in this guide (all FREE, no key needed):**
> | API | Base URL | What it gives |
> |-----|----------|---------------|
> | JSONPlaceholder | `https://jsonplaceholder.typicode.com` | Fake posts, users, todos |
> | httpbin | `https://httpbin.org` | Echo back your request |
> | Open-Meteo | `https://api.open-meteo.com` | Real weather data |
> | RestCountries | `https://restcountries.com` | Country info |

---

## Table of Contents

1. [What is the requests Module?](#1-what-is-the-requests-module)
2. [Installation & Import](#2-installation--import)
3. [GET Request — Fetch Data](#3-get-request--fetch-data)
4. [Query Parameters](#4-query-parameters)
5. [Response Object — All Properties](#5-response-object--all-properties)
6. [Request Headers](#6-request-headers)
7. [POST Request — Send Data](#7-post-request--send-data)
8. [PUT Request — Update Data](#8-put-request--update-data)
9. [PATCH Request — Partial Update](#9-patch-request--partial-update)
10. [DELETE Request — Remove Data](#10-delete-request--remove-data)
11. [Error Handling & Timeouts](#11-error-handling--timeouts)
12. [Sessions](#12-sessions)
13. [Real-World Mini Projects](#13-real-world-mini-projects)
14. [Self-Study Exercises — Level 1](#14-self-study-exercises--level-1)
15. [Quick Cheat Sheet](#15-quick-cheat-sheet)

---

## 1. What is the `requests` Module?

The `requests` module lets Python **talk to the internet** — fetch web pages, call APIs, send data to servers.

Think of it like this:

```
Your Python Script  →  requests  →  Internet / API  →  JSON response back
```

### HTTP Methods at a Glance

| Method | Purpose | Example |
|--------|---------|---------|
| `GET` | Fetch / Read data | Get list of users |
| `POST` | Create new data | Add a new post |
| `PUT` | Replace existing data | Update full profile |
| `PATCH` | Update part of data | Change only the name |
| `DELETE` | Remove data | Delete a post |

---

## 2. Installation & Import

```bash
# Install (one time only)
pip install requests
```

```python
# Import in your script
import requests
```

---

## 3. GET Request — Fetch Data

The most common request — just **read** data from an API.

### 3.1 Simplest GET

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

response = requests.get(url)

print(response.status_code)    # 200
print(response.json())
```

**Output:**
```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident...",
  "body": "quia et suscipit\nsuscipit recusandae..."
}
```

### 3.2 GET a List of Items

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

response = requests.get(url)
posts = response.json()

print(f"Total posts: {len(posts)}")         # Total posts: 100

# Print first 3 posts
for post in posts[:3]:
    print(f"  [{post['id']}] {post['title'][:50]}")
```

**Output:**
```
Total posts: 100
  [1] sunt aut facere repellat provident occaecati excep
  [2] qui est esse
  [3] ea molestiae et quasi eos aperiam iure qui aut
```

### 3.3 GET with Real Weather API (Open-Meteo — No Key!)

```python
import requests

url = "https://api.open-meteo.com/v1/forecast"

params = {
    "latitude":  17.38,       # Hyderabad latitude
    "longitude": 78.47,       # Hyderabad longitude
    "current":   "temperature_2m,wind_speed_10m,relative_humidity_2m",
    "timezone":  "Asia/Kolkata"
}

response = requests.get(url, params=params)
data = response.json()

current = data["current"]
print("=== Hyderabad Weather ===")
print(f"Temperature : {current['temperature_2m']} °C")
print(f"Humidity    : {current['relative_humidity_2m']} %")
print(f"Wind Speed  : {current['wind_speed_10m']} km/h")
```

**Output:**
```
=== Hyderabad Weather ===
Temperature : 32.4 °C
Humidity    : 68 %
Wind Speed  : 14.2 km/h
```

---

## 4. Query Parameters

Query parameters filter or customize the API response. They appear after `?` in a URL.

```
https://api.example.com/posts?userId=1&limit=5
                                ^^^^^^   ^^^^^^^
                               param 1   param 2
```

### 4.1 Passing params as a Dictionary (Recommended)

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

# Get only posts written by userId = 1
params = {"userId": 1}
response = requests.get(url, params=params)
posts = response.json()

print(f"Posts by user 1: {len(posts)}")    # 10

# requests builds the URL automatically:
print(response.url)
# https://jsonplaceholder.typicode.com/posts?userId=1

for post in posts[:3]:
    print(f"  [{post['id']}] {post['title'][:40]}")
```

**Output:**
```
Posts by user 1: 10
https://jsonplaceholder.typicode.com/posts?userId=1
  [1] sunt aut facere repellat provident
  [2] qui est esse
  [3] ea molestiae et quasi eos aperiam i
```

### 4.2 Multiple Parameters

```python
import requests

# Get todos that are completed, for user 1
url = "https://jsonplaceholder.typicode.com/todos"

params = {
    "userId":    1,
    "completed": True
}

response = requests.get(url, params=params)
todos = response.json()

print(f"Completed todos for user 1: {len(todos)}")
for todo in todos[:3]:
    print(f"  ✅ {todo['title']}")
```

**Output:**
```
Completed todos for user 1: 11
  ✅ delectus aut autem
  ✅ quis ut nam facilis et officia qui
  ✅ fugiat veniam minus
```

### 4.3 Country Search with RestCountries

```python
import requests

# Search for India
url = "https://restcountries.com/v3.1/name/india"
response = requests.get(url)
data = response.json()

country = data[0]
print(f"Name       : {country['name']['common']}")
print(f"Capital    : {country['capital'][0]}")
print(f"Population : {country['population']:,}")
print(f"Region     : {country['region']}")
print(f"Currency   : {list(country['currencies'].keys())[0]}")
```

**Output:**
```
Name       : India
Capital    : New Delhi
Population : 1,380,004,385
Region     : Asia
Currency   : INR
```

---

## 5. Response Object — All Properties

After every request, you get a **Response object** packed with useful info.

```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/users/1")

# ── STATUS ────────────────────────────────────────
print(response.status_code)        # 200
print(response.ok)                 # True  (True if status < 400)
print(response.reason)             # OK

# ── CONTENT ───────────────────────────────────────
print(type(response.text))         # <class 'str'>  — response as string
print(type(response.content))      # <class 'bytes'> — raw bytes
print(type(response.json()))       # <class 'dict'>  — parsed JSON ✅

# ── HEADERS ───────────────────────────────────────
print(response.headers)            # dict of response headers
print(response.headers["Content-Type"])   # application/json; charset=utf-8

# ── URL ───────────────────────────────────────────
print(response.url)                # https://jsonplaceholder.typicode.com/users/1

# ── TIMING ────────────────────────────────────────
print(response.elapsed)            # time taken for the request

# ── ENCODING ──────────────────────────────────────
print(response.encoding)           # utf-8
```

### Common HTTP Status Codes

| Code | Meaning |
|------|---------|
| `200` | OK — success |
| `201` | Created — POST success |
| `204` | No Content — DELETE success |
| `400` | Bad Request — your request has errors |
| `401` | Unauthorized — invalid/missing API key |
| `403` | Forbidden — you don't have permission |
| `404` | Not Found — wrong URL |
| `429` | Too Many Requests — rate limited |
| `500` | Internal Server Error — server problem |

```python
import requests

# Test different status codes using httpbin
for code in [200, 201, 404, 500]:
    r = requests.get(f"https://httpbin.org/status/{code}")
    icon = "✅" if r.ok else "❌"
    print(f"  {icon} {code} → {r.reason}")
```

**Output:**
```
  ✅ 200 → OK
  ✅ 201 → CREATED
  ❌ 404 → NOT FOUND
  ❌ 500 → INTERNAL SERVER ERROR
```

---

## 6. Request Headers

Headers send **extra information** to the server — like who you are, what format you want, or your API key.

### 6.1 Viewing Default Request Headers

```python
import requests

# httpbin.org echoes back everything about your request
response = requests.get("https://httpbin.org/headers")
data = response.json()

print("Default headers sent by requests:")
for key, val in data["headers"].items():
    print(f"  {key}: {val}")
```

**Output:**
```
Default headers sent by requests:
  Accept: */*
  Accept-Encoding: gzip, deflate, br
  Host: httpbin.org
  User-Agent: python-requests/2.31.0
```

### 6.2 Sending Custom Headers

```python
import requests

url = "https://httpbin.org/headers"

# Custom headers — e.g. for a RapidAPI call you'd add X-RapidAPI-Key here
headers = {
    "User-Agent":    "MyPythonApp/1.0",
    "Accept":        "application/json",
    "X-Custom-Info": "Learning Python APIs"
}

response = requests.get(url, headers=headers)
data = response.json()

print("Headers received by server:")
for key, val in data["headers"].items():
    print(f"  {key}: {val}")
```

**Output:**
```
Headers received by server:
  Accept: application/json
  Host: httpbin.org
  User-Agent: MyPythonApp/1.0
  X-Custom-Info: Learning Python APIs
```

### 6.3 How RapidAPI Headers Look (Template)

When you use any RapidAPI service, the headers follow this pattern:

```python
import requests

# ── RapidAPI header template ──────────────────────────────
headers = {
    "X-RapidAPI-Key":  "YOUR_API_KEY_HERE",        # from RapidAPI dashboard
    "X-RapidAPI-Host": "some-api.p.rapidapi.com"   # from API docs
}

url = "https://some-api.p.rapidapi.com/endpoint"
response = requests.get(url, headers=headers)
print(response.json())
# ─────────────────────────────────────────────────────────

# Demo with httpbin (no real key needed — just shows the pattern)
demo_headers = {
    "X-RapidAPI-Key":  "demo-key-12345",
    "X-RapidAPI-Host": "demo-api.p.rapidapi.com",
    "Content-Type":    "application/json"
}

r = requests.get("https://httpbin.org/headers", headers=demo_headers)
sent = r.json()["headers"]
print(f"Key header seen by server : {sent.get('X-Rapidapi-Key')}")
print(f"Host header seen by server: {sent.get('X-Rapidapi-Host')}")
```

**Output:**
```
Key header seen by server : demo-key-12345
Host header seen by server: demo-api.p.rapidapi.com
```

---

## 7. POST Request — Send Data

POST sends data **to** the server to create something new.

### 7.1 POST JSON Data

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts"

# Data to send
new_post = {
    "title":  "Learning Python APIs",
    "body":   "The requests module makes it super easy to call APIs.",
    "userId": 1
}

response = requests.post(url, json=new_post)

print(f"Status Code : {response.status_code}")   # 201 Created
print(f"Response    : {response.json()}")
```

**Output:**
```
Status Code : 201
Response    : {
  'title': 'Learning Python APIs',
  'body': 'The requests module makes it super easy to call APIs.',
  'userId': 1,
  'id': 101
}
```

### 7.2 POST with httpbin — See Exactly What Was Sent

```python
import requests

url = "https://httpbin.org/post"

payload = {
    "name":  "Alex",
    "email": "alex@example.com",
    "score": 95
}

headers = {"Content-Type": "application/json"}

response = requests.post(url, json=payload, headers=headers)
data = response.json()

print("What the server received:")
print(f"  JSON body : {data['json']}")
print(f"  Headers   : {data['headers']['Content-Type']}")
print(f"  Origin IP : {data['origin']}")
```

**Output:**
```
What the server received:
  JSON body : {'name': 'Alex', 'email': 'alex@example.com', 'score': 95}
  Headers   : application/json
  Origin IP : 203.x.x.x
```

### 7.3 POST Form Data (like an HTML form)

```python
import requests

url = "https://httpbin.org/post"

# Form data — use data= (not json=)
form_data = {
    "username": "alex123",
    "password": "secret",
    "action":   "login"
}

response = requests.post(url, data=form_data)
data = response.json()

print(f"Form data received: {data['form']}")
# Content-Type is automatically set to application/x-www-form-urlencoded
print(f"Content-Type: {data['headers']['Content-Type']}")
```

**Output:**
```
Form data received: {'username': 'alex123', 'password': 'secret', 'action': 'login'}
Content-Type: application/x-www-form-urlencoded
```

---

## 8. PUT Request — Update Data

PUT **replaces** the entire resource with new data.

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

# Complete replacement of post with id=1
updated_post = {
    "id":     1,
    "title":  "Updated Title — Python is Amazing",
    "body":   "This post has been completely replaced.",
    "userId": 1
}

response = requests.put(url, json=updated_post)

print(f"Status : {response.status_code}")   # 200
result = response.json()
print(f"ID     : {result['id']}")
print(f"Title  : {result['title']}")
print(f"Body   : {result['body']}")
```

**Output:**
```
Status : 200
ID     : 1
Title  : Updated Title — Python is Amazing
Body   : This post has been completely replaced.
```

---

## 9. PATCH Request — Partial Update

PATCH updates **only the fields you send** — the rest stay unchanged.

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

# Only update the title — body and userId remain unchanged
patch_data = {
    "title": "Only the title was changed by PATCH"
}

response = requests.patch(url, json=patch_data)

print(f"Status : {response.status_code}")   # 200
result = response.json()
print(f"ID     : {result['id']}")
print(f"Title  : {result['title']}")
# Note: body and userId still exist (unchanged)
print(f"UserId : {result['userId']}")
```

**Output:**
```
Status : 200
ID     : 1
Title  : Only the title was changed by PATCH
UserId : 1
```

### PUT vs PATCH — Key Difference

```python
# PUT — you must send ALL fields; missing fields get wiped
put_data  = {"id": 1, "title": "New", "body": "Full body", "userId": 1}

# PATCH — send only what changed; rest stays intact
patch_data = {"title": "Just the title changed"}
```

---

## 10. DELETE Request — Remove Data

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/1"

response = requests.delete(url)

print(f"Status Code : {response.status_code}")   # 200
print(f"Response    : {response.json()}")         # {} (empty — it's deleted)
print(f"Success     : {response.ok}")             # True
```

**Output:**
```
Status Code : 200
Response    : {}
Success     : True
```

> **Note:** JSONPlaceholder simulates deletion — the data isn't actually removed, but it returns the correct status code so you can practice.

---

## 11. Error Handling & Timeouts

### 11.1 Check Status Before Using Response

```python
import requests

def safe_get(url):
    response = requests.get(url)

    if response.status_code == 200:
        return response.json()
    elif response.status_code == 404:
        print(f"❌ Not Found: {url}")
    elif response.status_code == 500:
        print("❌ Server Error — try again later")
    else:
        print(f"❌ Unexpected status: {response.status_code}")
    return None

# Valid URL
data = safe_get("https://jsonplaceholder.typicode.com/users/1")
if data:
    print(f"✅ User: {data['name']}")

# Invalid URL — 404
safe_get("https://jsonplaceholder.typicode.com/users/9999")
```

**Output:**
```
✅ User: Leanne Graham
❌ Not Found: https://jsonplaceholder.typicode.com/users/9999
```

### 11.2 Using `raise_for_status()`

```python
import requests

url = "https://jsonplaceholder.typicode.com/posts/9999"

try:
    response = requests.get(url)
    response.raise_for_status()     # raises HTTPError if status >= 400
    print(response.json())

except requests.exceptions.HTTPError as e:
    print(f"HTTP Error: {e}")
except requests.exceptions.ConnectionError:
    print("No internet connection!")
except requests.exceptions.Timeout:
    print("Request timed out!")
except requests.exceptions.RequestException as e:
    print(f"Something went wrong: {e}")
```

**Output:**
```
HTTP Error: 404 Client Error: Not Found for url: ...
```

### 11.3 Timeout — Don't Wait Forever

```python
import requests

url = "https://httpbin.org/delay/3"   # this endpoint delays 3 seconds

try:
    # timeout=2 means: give up if no response in 2 seconds
    response = requests.get(url, timeout=2)
    print(response.json())

except requests.exceptions.Timeout:
    print("⏱ Request timed out after 2 seconds")
```

**Output:**
```
⏱ Request timed out after 2 seconds
```

### 11.4 Set Both Connect and Read Timeout

```python
import requests

# (connect_timeout, read_timeout) — both in seconds
response = requests.get(
    "https://jsonplaceholder.typicode.com/posts/1",
    timeout=(3, 5)      # 3s to connect, 5s to read response
)
print(response.status_code)    # 200
```

---

## 12. Sessions

A **Session** reuses the same connection and lets you set headers/params once for all requests.

### 12.1 Basic Session

```python
import requests

# Without Session — headers set each time
r1 = requests.get("https://httpbin.org/get", headers={"User-Agent": "MyApp"})
r2 = requests.get("https://httpbin.org/get", headers={"User-Agent": "MyApp"})

# With Session — set once, used everywhere ✅
session = requests.Session()
session.headers.update({
    "User-Agent": "MyPythonApp/1.0",
    "Accept":     "application/json"
})

r1 = session.get("https://httpbin.org/get")
r2 = session.get("https://jsonplaceholder.typicode.com/posts/1")

print(r1.json()["headers"]["User-Agent"])   # MyPythonApp/1.0
print(r2.json()["title"][:30])              # sunt aut facere...
```

### 12.2 Session with Base URL Pattern (RapidAPI Style)

```python
import requests

# For RapidAPI, you'd do this:
session = requests.Session()
session.headers.update({
    "X-RapidAPI-Key":  "YOUR_KEY_HERE",
    "X-RapidAPI-Host": "some-api.p.rapidapi.com"
})

# Then all calls automatically carry the key
# r1 = session.get("https://some-api.p.rapidapi.com/endpoint1")
# r2 = session.get("https://some-api.p.rapidapi.com/endpoint2")

# Demo version using httpbin
session2 = requests.Session()
session2.headers.update({"X-Session-Token": "abc123"})

r = session2.get("https://httpbin.org/headers")
print(r.json()["headers"].get("X-Session-Token"))   # abc123

session2.close()    # Always close the session when done
```

### 12.3 Session with Context Manager (Best Practice)

```python
import requests

with requests.Session() as session:
    session.headers.update({"Accept": "application/json"})

    # All requests in this block share the session
    users = session.get("https://jsonplaceholder.typicode.com/users")
    posts = session.get("https://jsonplaceholder.typicode.com/posts?userId=1")

    print(f"Total users : {len(users.json())}")
    print(f"Posts (u=1) : {len(posts.json())}")
# Session is automatically closed here
```

**Output:**
```
Total users : 10
Posts (u=1) : 10
```

---

## 13. Real-World Mini Projects

### Project 1: Weather Dashboard — Hyderabad

```python
import requests

def get_weather(city_lat, city_lon, city_name):
    url = "https://api.open-meteo.com/v1/forecast"
    params = {
        "latitude":        city_lat,
        "longitude":       city_lon,
        "current":         "temperature_2m,relative_humidity_2m,wind_speed_10m,weather_code",
        "daily":           "temperature_2m_max,temperature_2m_min",
        "timezone":        "Asia/Kolkata",
        "forecast_days":   3
    }
    r = requests.get(url, params=params, timeout=10)
    r.raise_for_status()
    return r.json()

data = get_weather(17.38, 78.47, "Hyderabad")
current = data["current"]
daily   = data["daily"]

print("╔══════════════════════════════╗")
print("║    🌤 Hyderabad Weather       ║")
print("╠══════════════════════════════╣")
print(f"║  Temp      : {current['temperature_2m']}°C              ║")
print(f"║  Humidity  : {current['relative_humidity_2m']}%              ║")
print(f"║  Wind      : {current['wind_speed_10m']} km/h           ║")
print("╠══════════════════════════════╣")
print("║  3-Day Forecast              ║")
for i in range(3):
    date  = daily["time"][i]
    hi    = daily["temperature_2m_max"][i]
    lo    = daily["temperature_2m_min"][i]
    print(f"║  {date}  ↑{hi}° ↓{lo}°   ║")
print("╚══════════════════════════════╝")
```

**Output:**
```
╔══════════════════════════════╗
║    🌤 Hyderabad Weather       ║
╠══════════════════════════════╣
║  Temp      : 32.4°C          ║
║  Humidity  : 68%             ║
║  Wind      : 14.2 km/h       ║
╠══════════════════════════════╣
║  3-Day Forecast              ║
║  2024-06-20  ↑35.1° ↓26.3°  ║
║  2024-06-21  ↑34.8° ↓25.9°  ║
║  2024-06-22  ↑33.5° ↓25.1°  ║
╚══════════════════════════════╝
```

---

### Project 2: Country Info Lookup

```python
import requests

def get_country(name):
    url = f"https://restcountries.com/v3.1/name/{name}"
    try:
        r = requests.get(url, timeout=10)
        r.raise_for_status()
        c = r.json()[0]

        currencies = ", ".join(c.get("currencies", {}).keys())
        languages  = ", ".join(c.get("languages", {}).values())

        print(f"\n🌍 {c['name']['common']} ({c['name']['official']})")
        print(f"   Capital    : {c.get('capital', ['N/A'])[0]}")
        print(f"   Region     : {c['region']} / {c.get('subregion','')}")
        print(f"   Population : {c['population']:,}")
        print(f"   Area       : {c.get('area', 0):,.0f} km²")
        print(f"   Currency   : {currencies}")
        print(f"   Languages  : {languages}")
        print(f"   Calling    : +{c.get('idd',{}).get('root','?')}")

    except requests.exceptions.HTTPError:
        print(f"Country '{name}' not found.")

get_country("india")
get_country("japan")
```

**Output:**
```
🌍 India (Republic of India)
   Capital    : New Delhi
   Region     : Asia / Southern Asia
   Population : 1,380,004,385
   Area       : 3,287,590 km²
   Currency   : INR
   Languages  : Hindi, English
   Calling    : +9

🌍 Japan (Japan)
   Capital    : Tokyo
   Region     : Asia / Eastern Asia
   Population : 125,836,021
   Area       : 377,930 km²
   Currency   : JPY
   Languages  : Japanese
   Calling    : +8
```

---

### Project 3: Fake Blog API — Full CRUD Demo

```python
import requests

BASE = "https://jsonplaceholder.typicode.com"

print("=== Blog CRUD Demo ===\n")

# CREATE — POST
print("1. CREATE a new post")
new = requests.post(f"{BASE}/posts", json={
    "title": "My Python API Post",
    "body":  "Calling APIs is easy with requests!",
    "userId": 1
})
post_id = new.json()["id"]
print(f"   Created post ID: {post_id}  Status: {new.status_code}\n")

# READ — GET
print("2. READ post #1")
post = requests.get(f"{BASE}/posts/1")
print(f"   Title: {post.json()['title'][:40]}\n")

# UPDATE — PUT
print("3. UPDATE (PUT) post #1 fully")
updated = requests.put(f"{BASE}/posts/1", json={
    "id":     1,
    "title":  "Fully replaced by PUT",
    "body":   "All fields sent in PUT.",
    "userId": 1
})
print(f"   New title: {updated.json()['title']}\n")

# PARTIAL UPDATE — PATCH
print("4. PARTIAL UPDATE (PATCH) post #1 title only")
patched = requests.patch(f"{BASE}/posts/1", json={
    "title": "Only title changed by PATCH"
})
print(f"   Patched title : {patched.json()['title']}")
print(f"   userId intact : {patched.json()['userId']}\n")

# DELETE
print("5. DELETE post #1")
deleted = requests.delete(f"{BASE}/posts/1")
print(f"   Status: {deleted.status_code}  Body: {deleted.json()}")
```

**Output:**
```
=== Blog CRUD Demo ===

1. CREATE a new post
   Created post ID: 101  Status: 201

2. READ post #1
   Title: sunt aut facere repellat provident

3. UPDATE (PUT) post #1 fully
   New title: Fully replaced by PUT

4. PARTIAL UPDATE (PATCH) post #1 title only
   Patched title : Only title changed by PATCH
   userId intact : 1

5. DELETE post #1
   Status: 200  Body: {}
```

---

## 14. Self-Study Exercises — Level 1

**Exercise 1 — GET & Print**
Use `requests.get()` to fetch the user with ID `3` from JSONPlaceholder:
`https://jsonplaceholder.typicode.com/users/3`
Print their `name`, `email`, and `city` (inside `address`).

```python
# Expected Output:
# Name  : Clementine Bauch
# Email : Nathan@yesenia.net
# City  : McKenziehaven
```

---

**Exercise 2 — Query Parameters**
Fetch all todos for `userId=2` from:
`https://jsonplaceholder.typicode.com/todos`
using the `params` dictionary. Print how many are completed and how many are pending.

```python
# Expected Output:
# Total todos for user 2 : 20
# Completed : 8
# Pending   : 12
```

---

**Exercise 3 — POST Request**
Send a POST request to `https://jsonplaceholder.typicode.com/posts` to create a new post with:
- `title` = your own title
- `body`  = a short description
- `userId` = 5

Print the status code and the `id` of the created post.

```python
# Expected Output:
# Status : 201
# New post ID : 101
```

---

**Exercise 4 — Status Code & Error Handling**
Write a function `check_url(url)` that:
- Makes a GET request to the URL
- Prints `✅ OK` if status is 200
- Prints `❌ Not Found` if status is 404
- Prints `⚠️ Error: <code>` for anything else

Test with:
- `https://jsonplaceholder.typicode.com/posts/1` → should be ✅
- `https://jsonplaceholder.typicode.com/posts/9999` → should be ❌

---

**Exercise 5 — Real Weather**
Use the Open-Meteo API to get the current temperature for your city (or any city):

```
https://api.open-meteo.com/v1/forecast
  ?latitude=YOUR_LAT
  &longitude=YOUR_LON
  &current=temperature_2m
  &timezone=Asia/Kolkata
```

Print the result as: `Current temperature in [City]: X.X °C`

> Tip: Hyderabad → lat=17.38, lon=78.47 | Delhi → lat=28.61, lon=77.21 | Chennai → lat=13.08, lon=80.27

---

## 15. Quick Cheat Sheet

```python
import requests

# ── BASIC REQUESTS ────────────────────────────────────────────
r = requests.get(url)
r = requests.get(url, params={"key": "value"})       # with query params
r = requests.post(url, json={"key": "value"})         # POST JSON
r = requests.post(url, data={"key": "value"})         # POST form data
r = requests.put(url, json=payload)                   # PUT (full replace)
r = requests.patch(url, json={"field": "value"})      # PATCH (partial)
r = requests.delete(url)                              # DELETE

# ── HEADERS ───────────────────────────────────────────────────
headers = {
    "Content-Type":    "application/json",
    "X-RapidAPI-Key":  "YOUR_KEY",
    "X-RapidAPI-Host": "api.p.rapidapi.com"
}
r = requests.get(url, headers=headers)

# ── RESPONSE PROPERTIES ───────────────────────────────────────
r.status_code        # 200, 201, 404, 500 ...
r.ok                 # True if status_code < 400
r.text               # response as string
r.content            # response as bytes
r.json()             # response as dict/list ← most used
r.headers            # response headers dict
r.url                # final URL (including params)
r.elapsed            # time taken

# ── ERROR HANDLING ────────────────────────────────────────────
r.raise_for_status()   # raises HTTPError if status >= 400

try:
    r = requests.get(url, timeout=5)
    r.raise_for_status()
    data = r.json()
except requests.exceptions.HTTPError as e:    print(e)
except requests.exceptions.ConnectionError:   print("No internet")
except requests.exceptions.Timeout:           print("Timed out")
except requests.exceptions.RequestException:  print("Unknown error")

# ── SESSION ───────────────────────────────────────────────────
with requests.Session() as s:
    s.headers.update({"X-RapidAPI-Key": "key"})
    r = s.get(url)
```

---

*End of Week-04 Day-19 — `requests` Module*
