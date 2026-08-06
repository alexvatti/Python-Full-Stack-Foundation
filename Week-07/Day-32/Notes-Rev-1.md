# Week-07

# Day-32

# MySQL CRUD Operations using Modular Programming

---

# Project Structure

```
Day-32

│

├── config.py

├── database.py

├── create_table.py

├── insert_record.py

├── insert_multiple.py

├── select_records.py

├── update_record.py

├── delete_record.py

├── search_record.py

├── order_by.py

├── limit_records.py

└── README.md
```

---

# Why Modular Programming?

Instead of writing the MySQL connection code in every program,

we write it only once.

All other Python programs simply import the connection function.

---

# Advantages

✅ Less Code

✅ Easy to Maintain

✅ Reusable

✅ Professional Coding Style

✅ Industry Standard

---

# Step-1

## Create config.py

Store the database credentials.

```python
HOST = "sql12.freesqldatabase.com"

DATABASE = "sql12834641"

USER = "sql12834641"

PASSWORD = "YOUR_PASSWORD"
```

Replace

```
YOUR_PASSWORD
```

with your actual password.

---

# Step-2

## Create database.py

This file contains the common database connection code.

Every program will use this file.

```python
import mysql.connector

from config import HOST
from config import DATABASE
from config import USER
from config import PASSWORD


def get_connection():

    connection = mysql.connector.connect(
        host=HOST,
        database=DATABASE,
        user=USER,
        password=PASSWORD
    )

    return connection
```

---

# How to Use

Instead of writing

```python
connection = mysql.connector.connect(
    host="...",
    database="...",
    user="...",
    password="..."
)
```

simply write

```python
from database import get_connection

connection = get_connection()
```

That's it.

---

# Common Template

Every program will follow this structure.

```python
from database import get_connection


def main():

    connection = get_connection()

    cursor = connection.cursor()

    # SQL Statements

    connection.commit()

    cursor.close()

    connection.close()


if __name__ == "__main__":
    main()
```

---

# Example

## insert_record.py

```python
from database import get_connection


def main():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
    INSERT INTO Student(name,department,marks)
    VALUES(%s,%s,%s)
    """

    values = ("Alex","CSE",91)

    cursor.execute(sql, values)

    connection.commit()

    print("Record Inserted Successfully")

    cursor.close()

    connection.close()


if __name__ == "__main__":
    main()
```

---

# Example

## select_records.py

```python
from database import get_connection


def main():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("SELECT * FROM Student")

    rows = cursor.fetchall()

    for row in rows:
        print(row)

    cursor.close()

    connection.close()


if __name__ == "__main__":
    main()
```

---

# Workflow

```
config.py

        │

        ▼

database.py

        │

        ▼

All Python Programs

        │

        ├── create_table.py

        ├── insert_record.py

        ├── insert_multiple.py

        ├── select_records.py

        ├── update_record.py

        ├── delete_record.py

        ├── search_record.py

        ├── order_by.py

        └── limit_records.py
```

---

# Best Practices

- Store credentials only in `config.py`.
- Create the connection only through `database.py`.
- Close the cursor after every operation.
- Close the connection after every operation.
- Use parameterized queries (`%s`) for user input.
- Commit changes after `INSERT`, `UPDATE`, and `DELETE`.
- Keep one task per Python file.

---

# What You Will Learn Next

Using the common connection module, we will implement:

1. Create Table
2. Insert One Record
3. Insert Multiple Records
4. Select All Records
5. Search Using WHERE
6. ORDER BY
7. LIMIT
8. Update Record
9. Delete Record
10. Complete CRUD Menu Program

From Day-32 onward, every MySQL program will use the same `config.py` and `database.py` files. This avoids repeating connection code and reflects the modular structure used in professional Python applications.
