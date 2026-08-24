# Database Normalization: 1NF, 2NF, 3NF

Normalization is the process of organizing a flat, redundant table into smaller, well-structured tables that reduce data duplication and prevent update anomalies (inconsistent data when you insert, update, or delete records).

This document walks through the three most common normal forms — **1NF**, **2NF**, and **3NF** — using two worked examples.

---

## What Each Normal Form Fixes

| Normal Form | Problem It Solves | Rule |
|-------------|-------------------|------|
| **1NF** | Multiple values stuffed into one cell | Every cell must hold a single, atomic value |
| **2NF** | Columns depending on only part of a composite key | Non-key columns must depend on the **whole** primary key |
| **3NF** | Columns depending on other non-key columns | Non-key columns must depend **only** on the primary key, not on each other |

---

## Example 1: Orders and Products

### Flat (Unnormalized) Table

| OrderID | CustomerName | CustomerCity | ProductID | ProductName | ProductPrice | Qty |
|---------|-------------|--------------|-----------|-------------|---------------|-----|
| 101 | Alex | Hyderabad | P1, P2 | Pen, Book | 10, 200 | 5, 2 |
| 102 | Riya | Mumbai | P3 | Bag | 500 | 1 |

**Problem:** The `ProductID`, `ProductName`, `ProductPrice`, and `Qty` columns each hold multiple values in a single cell for Order 101. This is called a **repeating group** and violates the basic rule of relational tables.

---

### Step 1 — First Normal Form (1NF)

**Rule:** Each cell must hold a single (atomic) value. No repeating groups, no comma-separated lists.

**Fix:** Split the repeating group into separate rows — one row per product per order.

| OrderID | CustomerName | CustomerCity | ProductID | ProductName | ProductPrice | Qty |
|---------|-------------|--------------|-----------|-------------|---------------|-----|
| 101 | Alex | Hyderabad | P1 | Pen | 10 | 5 |
| 101 | Alex | Hyderabad | P2 | Book | 200 | 2 |
| 102 | Riya | Mumbai | P3 | Bag | 500 | 1 |

✅ Every cell now has exactly one value → the table is in **1NF**.

⚠️ Remaining issue: `CustomerName` and `CustomerCity` are repeated for every product in the same order. Data redundancy still exists.

---

### Step 2 — Second Normal Form (2NF)

**Rule:** Table must already be in 1NF, and every non-key column must depend on the **entire** primary key — not just part of it. This only matters when the primary key is composite (made of 2+ columns).

**Analysis:** The primary key here is **(OrderID, ProductID)**.
- `CustomerName` and `CustomerCity` depend only on `OrderID` → **partial dependency**
- `ProductName` and `ProductPrice` depend only on `ProductID` → **partial dependency**

**Fix:** Split into three tables so each column sits with the key it actually depends on.

**`Orders`**

| OrderID | CustomerName | CustomerCity |
|---------|-------------|--------------|
| 101 | Alex | Hyderabad |
| 102 | Riya | Mumbai |

**`Products`**

| ProductID | ProductName | ProductPrice |
|-----------|-------------|---------------|
| P1 | Pen | 10 |
| P2 | Book | 200 |
| P3 | Bag | 500 |

**`OrderDetails`** (links Orders and Products)

| OrderID | ProductID | Qty |
|---------|-----------|-----|
| 101 | P1 | 5 |
| 101 | P2 | 2 |
| 102 | P3 | 1 |

✅ No column depends on only part of a composite key → the tables are in **2NF**.

---

### Step 3 — Third Normal Form (3NF)

**Rule:** Table must already be in 2NF, and no non-key column may depend on another non-key column (a **transitive dependency**).

**Analysis:** Suppose we add `CustomerState`, derived from `CustomerCity` (e.g., Hyderabad → Telangana). If stored inside `Orders`, then:
- `CustomerState` depends on `CustomerCity`
- `CustomerCity` depends on `OrderID`

So `CustomerState` depends on `OrderID` only *indirectly*, through `CustomerCity` — a transitive dependency.

**Fix:** Pull the city/state relationship into its own table.

**`Customers`**

| CustomerName | CustomerCity |
|-------------|--------------|
| Alex | Hyderabad |
| Riya | Mumbai |

**`Cities`**

| CustomerCity | CustomerState |
|--------------|----------------|
| Hyderabad | Telangana |
| Mumbai | Maharashtra |

**`Orders`** (now only references the customer)

| OrderID | CustomerName |
|---------|-------------|
| 101 | Alex |
| 102 | Riya |

✅ Every non-key column now depends only on its own table's primary key → the tables are in **3NF**.

---

### Final Table Set (Example 1)

`Customers` · `Cities` · `Orders` · `OrderDetails` · `Products`

Each table represents exactly one entity. Updating a product's price or a customer's city now only requires changing **one row**, in **one place**.

---

## Example 2: Students and Courses

### Flat (Unnormalized) Table

| StudentID | StudentName | Courses | Instructor | InstructorPhone |
|-----------|-------------|---------|-------------|------------------|
| S1 | Meera | Math, Physics | Mr. Rao, Mr. Iyer | 9876543210, 9123456789 |
| S2 | Kabir | Chemistry | Ms. Sen | 9988776655 |

**Problem:** `Courses`, `Instructor`, and `InstructorPhone` each pack multiple values into one cell for Meera, who is enrolled in two courses.

---

### Step 1 — First Normal Form (1NF)

**Fix:** One row per student-course combination.

| StudentID | StudentName | Course | Instructor | InstructorPhone |
|-----------|-------------|--------|-------------|------------------|
| S1 | Meera | Math | Mr. Rao | 9876543210 |
| S1 | Meera | Physics | Mr. Iyer | 9123456789 |
| S2 | Kabir | Chemistry | Ms. Sen | 9988776655 |

✅ Every cell holds one value. Primary key = **(StudentID, Course)** → table is in **1NF**.

---

### Step 2 — Second Normal Form (2NF)

**Analysis:**
- `StudentName` depends only on `StudentID` → partial dependency
- `Instructor` and `InstructorPhone` depend only on `Course` → partial dependency

**Fix:** Split into three tables.

**`Students`**

| StudentID | StudentName |
|-----------|-------------|
| S1 | Meera |
| S2 | Kabir |

**`Courses`**

| Course | Instructor | InstructorPhone |
|--------|-------------|------------------|
| Math | Mr. Rao | 9876543210 |
| Physics | Mr. Iyer | 9123456789 |
| Chemistry | Ms. Sen | 9988776655 |

**`Enrollments`** (links Students and Courses)

| StudentID | Course |
|-----------|--------|
| S1 | Math |
| S1 | Physics |
| S2 | Chemistry |

✅ No column depends on only part of the composite key → tables are in **2NF**.

---

### Step 3 — Third Normal Form (3NF)

**Analysis:** In `Courses`, `InstructorPhone` depends on `Instructor` (not directly on `Course`) — a transitive dependency. If Mr. Rao teaches multiple subjects, his phone number would be duplicated and could go out of sync.

**Fix:** Separate instructors into their own table.

**`Courses`**

| Course | Instructor |
|--------|-------------|
| Math | Mr. Rao |
| Physics | Mr. Iyer |
| Chemistry | Ms. Sen |

**`Instructors`**

| Instructor | InstructorPhone |
|-------------|------------------|
| Mr. Rao | 9876543210 |
| Mr. Iyer | 9123456789 |
| Ms. Sen | 9988776655 |

✅ Every non-key column depends only on its table's own primary key → tables are in **3NF**.

---

### Final Table Set (Example 2)

`Students` · `Courses` · `Instructors` · `Enrollments`

Changing Mr. Rao's phone number now requires updating **one row** in `Instructors`, instead of hunting through every course row he's linked to.

---

## Quick Recap

| Step | Question to Ask | Fix |
|------|------------------|-----|
| **1NF** | Does any cell hold more than one value? | Split into separate rows |
| **2NF** | Does a column depend on only *part* of the primary key? | Move it to a table keyed by that part |
| **3NF** | Does a non-key column depend on *another* non-key column? | Move it to its own table |

**Net result:** smaller, single-purpose tables, minimal redundancy, and updates that only ever need to happen in one place.
