
# Week 1 | Day 6 Mission: Completing the In-Memory CRUD Skeleton (C & R Integration)

## 💡 Core Problem Identification

> **[Problem]** We need to integrate the **GET (Retrieve Data)** and **POST (Create Data)** functionalities learned in Week 1 to be handled at a **single address (`/`)**. The goal is to complete the **most basic web application skeleton (C & R)** that actually works, and clearly recognize the limitation of data volatility.

## 🛠️ Targeted Goal

1.  Configure the **`/` route** with `methods=['GET', 'POST']` to branch and handle both requests within one function.
2.  Use a **`memo_data`** list for temporary data storage and management in the server's memory (**In-Memory DB Simulation**).
3.  Apply the **PRG Pattern (POST-Redirect-GET)** after data processing to ensure a safe and clean user experience.

-----

## 🔑 Key Learning: The Server's Dual Role (GET & POST Integration)

### 1\. Global Variables: Temporary Data Storage

Since a real database is not yet in use, we use a Python **global list** (`memo_data`) as temporary storage; the data persists only while the server is running. Each memo is stored as a **dictionary** with an `id`.

> **Caution:** Declaring `global next_id` is absolutely necessary to **modify** the value of the global variable inside the function.

### 2\. Branching Request Methods within a Function

Within a single View Function (`memo_list`), we check **`request.method`** to completely separate the logic based on the purpose of the incoming request.

  * **`if request.method == 'POST'` (Data Creation):**
      * Receive the form data from the user (`request.form.get('memo_content')`).
      * Assign a new ID and **append** the new memo to the `memo_data` list (the temporary DB).
      * **Redirect** the user.
  * **`else` (GET Request):**
      * **Retrieve all data** from `memo_data`.
      * Use `render_template()` to pass the data to the template and display the **list**.

-----

## 💻 1. Python Server Code (`app.py`)

```python
# 1. Import all necessary modules
from flask import Flask, request, redirect, url_for, render_template, flash

# 2. Create the Flask app and set the secret key for session management (essential for flash messages)
app = Flask(__name__)
app.secret_key = 'pbl_week1_final' 

# 3. Define the list to act as the in-memory DB using global variables (data is lost upon server restart)
memo_data = [
    {'id': 1, 'content': 'Day 6 Mission: Integrate C and R functionalities'},
    {'id': 2, 'content': 'Recognize the necessity of Database learning in Week 2.'}
]
# Counter for assigning the ID of the next new memo
next_id = 3

# =========================================================
# 4. Integrated Routing for GET (Read) and POST (Create)
# =========================================================

# Allow both GET and POST requests to the '/' address.
@app.route('/', methods=['GET', 'POST'])
def memo_list():
    global next_id # Declare global to modify the global variable's value
    
    # 4-1. If the request is POST (User submits a form to send data to the server)
    if request.method == 'POST':
        content = request.form.get('memo_content') # Extract 'memo_content' data from the form
        
        if content:
            # Create a new memo object and add it to the list (temporary DB) (CREATE Logic)
            new_memo = {'id': next_id, 'content': content}
            memo_data.append(new_memo) 
            next_id += 1 # Prepare the next ID
            flash('New memo successfully registered.', 'success')
        
        # PRG Pattern: Redirect after data processing to switch to a GET request
        return redirect(url_for('memo_list'))

    # 4-2. If the request is GET (Page is first opened or after redirection)
    # Pass the data from the in-memory DB to the template to display the list (READ Logic)
    return render_template('6day_index.html', memos=memo_data)

# 5. Server Startup
if __name__ == '__main__':
    app.run(debug=True)
```

-----

## 💡 2. HTML Template Code (`templates/6day_index.html`)

This template performs two roles: sending a **POST request** via the form and displaying the **list** received from the server using a loop.

```html
{% extends "base.html" %}

{% block title %}Mini Memo App (Create & Read Integrated){% endblock %}

{% block content %}
    <h1>📝 Mini Memo App (C & R)</h1>

    <div style="border: 1px solid #ccc; padding: 15px; margin-bottom: 30px;">
        <h3>Write New Memo</h3>
        <form method="POST" action="/">
            <textarea name="memo_content" rows="3" cols="50" required 
                      placeholder="Write your new memo here."></textarea><br>
            <button type="submit">Register Memo</button>
        </form>
    </div>

    <h2>Registered Memo List (Total {{ memos|length }} items)</h2>
    {% if memos %}
        <ul style="list-style-type: disc; padding-left: 20px;">
            {% for memo in memos %}
            <li style="border: 1px solid #eee; padding: 10px; margin-bottom: 10px; background-color: #f9f9f9;">
                <strong>ID: {{ memo.id }}</strong><br>
                <p>{{ memo.content }}</p>
            </li>
            {% endfor %}
        </ul>
    {% else %}
        <p>No memos have been registered yet.</p>
    {% endif %}
    
    <p style="color: red; font-weight: bold;">[Problem Awareness] All this data will be lost if the server is restarted or shut down! 😩</p>

{% endblock %}
```

### How to Run

1.  Save `app.py` and `templates/6day_index.html` in the correct locations.
2.  Run the server with `python app.py` and check the operation in your browser.

-----

## 🎯 Day 6 Mission Completion and Deconstruction Learning

### 1\. Deconstructing the Code

  * **Role of `global`:** Try running the code without placing `global` before `next_id`. An error will occur, and `next_id` will not increment. You must understand why `global` is needed when **changing the value** of a global variable inside a function.
  * **PRG Mechanism:** After registering a memo, open the browser's Network tab (F12) and confirm that the requests switch from POST $\rightarrow$ 302 Redirect $\rightarrow$ GET. This is the **shield against duplicate submission**.
  * **Experiencing Volatility:** Add about five memos, then shut down and restart the server from the terminal. Witnessing all the memos disappear should strongly emphasize the **need for Database learning in Week 2**.

