
# Day 7 Mission: Final Review of Week 1 and Preparation for Database (DB)

## 💡 Core Problem Identification

> **[Problem]** The mini memo application from Day 6 has a **critical limitation**: the data disappears when the server is shut down. How should we prepare to overcome this limitation and effectively learn the technologies for **data persistence and management** (DB/SQL) that will start next week?

## 🛠️ Targeted Goal

1. Final review of Week 1 learning content (HTTP, Flask basics, Templates, PRG).
2. Define the **necessity and role of a Database (DB)**.
3. Review and summarize the basic concepts of **SQL CRUD**.

## 🔑 Key Learning: Week 1 Summary and Week 2 Preparation

| **Topic** | **What was Learned in Week 1** | **What will be Solved in Week 2** |
| :--- | :--- | :--- |
| **Communication** | HTTP (GET/POST), PRG Pattern, Redirection | Efficient data communication via API (RESTful API) |
| **Framework** | Flask basic setup, Routing, `render_template` | Structuring large-scale apps using Flask Blueprints |
| **Data** | In-Memory list storage, receiving data via `request.form` | **Permanent data storage and management (Solving volatility)** |

---

### **[Essential Prereading] Basic SQL Concepts** 💡

1.  **Role of the DB:** A system that stores data **permanently**, **efficiently**, and **safely**.
2.  **Table:** The storage space, similar to a spreadsheet (e.g., an Excel sheet).
3.  **Column:** The attribute or field of the table (e.g., Name, Age).
4.  **Row (Record):** A single piece of actual data (e.g., 'John Doe', 30).
5.  **SQL (Structured Query Language):** The language used to communicate with the database.
6.  **SQL CRUD:** The four fundamental operations for managing data:
    * **C**reate: `INSERT`
    * **R**ead: `SELECT`
    * **U**pdate: `UPDATE`
    * **D**elete: `DELETE` 

---

### 🎯 Deconstruction Learning Guide

* **Week 1 Review:** Review your written `app.py` code one more time, and explain which part of the HTTP Request-Response cycle each line corresponds to.
* **Week 2 Prereading:** Connect the **SQL CRUD verbs** with the **HTTP methods (GET, POST)** you used in Flask. (e.g., GET is similar to SQL's SELECT).
