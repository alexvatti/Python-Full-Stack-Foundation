# SQLite Database Operations using Functions and Menu

## Objective

Develop a menu-driven Python program using SQLite to perform the following operations:

- Create Tables
- Drop Table
- Truncate Table (Delete all Records)
- Show Tables
- Close Database Connection

---

# Python Program

```python
import sqlite3


# ======================================
# Database Connection
# ======================================

def db_connect():
    conn = sqlite3.connect("college.db")
    cursor = conn.cursor()
    print("\nDatabase Connected Successfully.\n")
    return conn, cursor


# ======================================
# Database Close
# ======================================

def db_close(conn):
    conn.close()
    print("\nDatabase Closed Successfully.\n")


# ======================================
# Create Tables
# ======================================

def create_tables(conn, cursor):

    cursor.execute("""
    CREATE TABLE IF NOT EXISTS Student(
        id INTEGER PRIMARY KEY,
        name TEXT,
        age INTEGER,
        branch TEXT,
        marks REAL
    )
    """)

    cursor.execute("""
    CREATE TABLE IF NOT EXISTS Employee(
        id INTEGER PRIMARY KEY,
        name TEXT,
        department TEXT,
        salary REAL
    )
    """)

    cursor.execute("""
    CREATE TABLE IF NOT EXISTS Product(
        id INTEGER PRIMARY KEY,
        product_name TEXT,
        price REAL,
        quantity INTEGER
    )
    """)

    cursor.execute("""
    CREATE TABLE IF NOT EXISTS Book(
        id INTEGER PRIMARY KEY,
        title TEXT,
        author TEXT,
        price REAL
    )
    """)

    cursor.execute("""
    CREATE TABLE IF NOT EXISTS Patient(
        id INTEGER PRIMARY KEY,
        name TEXT,
        age INTEGER,
        disease TEXT
    )
    """)

    conn.commit()

    print("Tables Created Successfully.")


# ======================================
# Drop Table
# ======================================

def drop_table(conn, cursor):

    table = input("Enter Table Name : ")

    cursor.execute(f"DROP TABLE IF EXISTS {table}")

    conn.commit()

    print("Table Dropped Successfully.")


# ======================================
# Truncate Table
# SQLite does not support TRUNCATE
# ======================================

def truncate_table(conn, cursor):

    table = input("Enter Table Name : ")

    cursor.execute(f"DELETE FROM {table}")

    conn.commit()

    print("All Records Deleted Successfully.")


# ======================================
# Show Tables
# ======================================

def show_tables(cursor):

    cursor.execute("""
    SELECT name
    FROM sqlite_master
    WHERE type='table'
    ORDER BY name
    """)

    tables = cursor.fetchall()

    print("\nAvailable Tables")
    print("-------------------------")

    if len(tables) == 0:
        print("No Tables Found.")

    else:
        for table in tables:
            print(table[0])


# ======================================
# Menu
# ======================================

def menu():

    conn, cursor = db_connect()

    while True:

        print("\n========== MENU ==========")
        print("1. Create Tables")
        print("2. Drop Table")
        print("3. Truncate Table")
        print("4. Show Tables")
        print("5. Exit")
        print("==========================")

        choice = input("Enter Choice : ")

        if choice == "1":
            create_tables(conn, cursor)

        elif choice == "2":
            drop_table(conn, cursor)

        elif choice == "3":
            truncate_table(conn, cursor)

        elif choice == "4":
            show_tables(cursor)

        elif choice == "5":
            db_close(conn)
            print("Thank You...")
            break

        else:
            print("Invalid Choice.")


# ======================================
# Main Program
# ======================================

menu()
```

---

# Function Hierarchy

```
menu()
│
├── db_connect()
│      ├── conn
│      └── cursor
│
├── create_tables(conn, cursor)
│
├── drop_table(conn, cursor)
│
├── truncate_table(conn, cursor)
│
├── show_tables(cursor)
│
└── db_close(conn)
```

---

# Sample Output

```
Database Connected Successfully.

========== MENU ==========
1. Create Tables
2. Drop Table
3. Truncate Table
4. Show Tables
5. Exit
==========================
Enter Choice : 1

Tables Created Successfully.


========== MENU ==========
1. Create Tables
2. Drop Table
3. Truncate Table
4. Show Tables
5. Exit
==========================
Enter Choice : 4

Available Tables
-------------------------
Book
Employee
Patient
Product
Student


========== MENU ==========
Enter Choice : 3

Enter Table Name : Student

All Records Deleted Successfully.


========== MENU ==========
Enter Choice : 2

Enter Table Name : Product

Table Dropped Successfully.


========== MENU ==========
Enter Choice : 5

Database Closed Successfully.

Thank You...
```

---

# Notes

- `db_connect()` establishes the SQLite database connection and returns both the connection object and cursor.
- `db_close()` closes the database connection.
- `conn.commit()` permanently saves changes made to the database.
- SQLite does **not** support the `TRUNCATE TABLE` command.
- `DELETE FROM table_name;` is used as the SQLite equivalent of `TRUNCATE TABLE`.
- The program is modular because every operation is implemented as a separate function.
- The menu runs continuously until the user selects the **Exit** option.

---
