# Day 8 Mission:: Database Fundamentals and First Steps

## 💡 Core Problem Identification

The mini memo app from Week 1 stored data only in Python variables (`list`, `dict`), causing all content in the server's memory (RAM) to vanish the moment the server was shut down.

❓ **The Challenge:** What is needed to store data in a **"never-fading storage"**?

❓ Furthermore, how do we manage complex data in a **structured and systematic way**?

-----

## ⭐ Daily Learning Goal (DLG)

✔ Understand the structure of **Relational Databases (RDB)**.

✔ Learn **SQL**—the "language for conversing with data."

✔ Create a real DB using **SQLite** and practice data storage/retrieval.

-----

## 🧩 Core Concepts: Relational Databases and SQL

### 1\) 🧱 Relational Database (RDB)

An RDB is a type of database that stores data in a **"table" format, similar to a spreadsheet.**

  * Data is saved in **Rows** and **Columns**.
  * Multiple tables can be linked together using defined **relationships**.
  * Manipulated using the **SQL language**.

| Term | Simple Explanation |
| :--- | :--- |
| **Table** | A single spreadsheet (e.g., `users`, `posts`) |
| **Column** | The name of each vertical field (e.g., `id`, `username`) |
| **Row (Record)** | A single line of actual data |
| **Schema** | The rules defining the table structure (column name, data type) |
| **PRIMARY KEY** | A unique identifier that **absolutely forbids duplication** for each row. |

### 2\) 💬 SQL (Structured Query Language)

SQL is the **official language** used to communicate with the database management system (DBMS). You should first understand these three core commands:

| SQL Command | Meaning | Simple Explanation |
| :--- | :--- | :--- |
| **CREATE TABLE** | Structure Creation | "Create a table with this specific shape." |
| **INSERT** | Data Insertion (C) | "Save these values\!" |
| **SELECT** | Data Reading (R) | "Show me this data\!" |

-----

## 🛠️ Practical Code (Basic SQLite SQL)

The following queries can be executed directly in a SQLite console or a tool like DB Browser.

```sql
-- 1) Create a table named 'users' (Define the Schema)
-- 'id' is the PRIMARY KEY (unique identifier)
-- 'username' must have a value (NOT NULL) and be unique
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username TEXT NOT NULL UNIQUE,
    email TEXT
);

-- 2) Insert two new people into the 'users' table (CREATE)
INSERT INTO users (username, email) 
VALUES ('dev_kim', 'dev@example.com');

INSERT INTO users (username, email) 
VALUES ('student_lee', 'lee@pbl.net');

-- 3) Retrieve all users (READ)
SELECT * FROM users;

-- 4) Retrieve only the user whose username is 'dev_kim' (READ with Condition)
SELECT * FROM users 
WHERE username = 'dev_kim';
```

### 🔍 Code Breakdown

  * **`CREATE TABLE`**: Creates the `users` "sheet."
      * `id` is the unique number $\rightarrow$ Cannot be duplicated.
      * `username` must be entered (NOT NULL) and must be UNIQUE.
  * **`INSERT`**: Adds a new record (row) to the `users` table.
  * **`SELECT`**: Checks the data in the table.
      * Uses **`WHERE`** to filter records when a condition is required.

-----

## 🧠 Mission Summary (Simplified)

Today is about creating the **permanent storage layer**.

  * Data is moved from **RAM** $\rightarrow$ **DB**.
  * The DB ensures data persistence even when the server is off.
  * **SQL** is the language for issuing commands to the DB.
  * We learned the structure (Schema) and data rules of a table.

### 🧪 Day 8 Mission Test

✔ Successfully create the `users` table.

✔ Insert two records into the table.

✔ Retrieve all records using `SELECT`.

✔ Search for specific records using `WHERE`.

