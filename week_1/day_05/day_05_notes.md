

# Day 5 Mission: Implementing Robust Request Handling with PRG Pattern

## 💡 Core Problem Identification

> **[Problem]** Although we successfully processed data on Day 3, a problem arises where data is resubmitted if the user stays on the POST request result page and refreshes. Furthermore, how can we cleanly display a **one-time message** such as **"Successfully Processed"** when a user completes an action?

## 🛠️ Targeted Goal

1.  Understand and implement the **POST-Redirect-GET (PRG)** pattern.
2.  Use Flask's **`redirect`** function and **`url_for`** function.
3.  Display a one-time (session-based) message using the **`flash`** function.
4.  Integrate **Static Files (CSS)** basics.

## 🔑 Key Learning: PRG Pattern and Flash Messages

  * **PRG (POST-Redirect-GET) Pattern:** This is the standard practice of commanding the client to **redirect** and make a subsequent GET request after processing a POST request. This resolves the page refresh data resubmission issue.
  * **`redirect(url_for('function_name'))`:** Commands the client to navigate to a specific URL. `url_for` converts a function name into its corresponding URL address, eliminating the need to modify code if the URL path changes.
  * **`flash`:** Stores a one-time message in the session. The message is retrieved and displayed on the next request (the Redirected GET request) and is immediately deleted afterward. **(Note: Setting `app.secret_key` in the Flask app is essential for session management.)**
  * **Static Files:** Fixed files like CSS, JS, and images should be placed in the **`static`** folder and accessed using `url_for('static', filename='...')`.

### 💻 Completed Solution Code (`app.py`, `base.html` modification)

#### 1\. `app.py` (Flask Server File)

```python
# 1. Import required functions: request, redirect, url_for, flash, get_flashed_messages, render_template
from flask import Flask, request, redirect, url_for, flash, get_flashed_messages, render_template

# 2. Create the Flask application object and set a secret key for flash messages.
app = Flask(__name__)
# This must be set to an arbitrary string for security. (Used for session management)
app.secret_key = 'super_secret_key_for_flash' 

# Temporary memo data (Pre-prepared for Day 6 mission)
memos = []

# =========================================================
# 3. Handle GET/POST Requests and Apply PRG Pattern
# =========================================================

@app.route('/', methods=['GET', 'POST'])
def home():
    if request.method == 'POST':
        # 3-1. POST: Data processing logic (Day 3 content)
        new_memo = request.form.get('memo_content')
        if new_memo:
            memos.append(new_memo) # Store data in memory (Pre-application of Day 6 content)
            
            # Use flash() to store a one-time success message in the session for the user.
            flash('New memo successfully registered!', 'success')
            
        # 3-2. PRG Pattern: After processing the data, mandate a redirect to ensure a GET request follows.
        # url_for('home') finds the 'home' function associated with the '/' address and returns the URL.
        return redirect(url_for('home'))
        
    # 3-3. GET: Page display logic
    # Code to retrieve and display flash messages must be added to the template. (Handled in base.html)
    return render_template('5day_index.html', memo_list=memos)

# 4. Server Startup
if __name__ == '__main__':
    app.run(debug=True)
```

#### 2\. `templates/5day_index.html` (Displaying the Form and List)

```html
{% extends 'base.html' %} 

{% block content %}
    <h1>Day 5: Redirects and Messages</h1>
    
    <form method="POST" action="{{ url_for('home') }}">
        <label for="memo_content">New Memo:</label><br>
        <input type="text" id="memo_content" name="memo_content" required>
        <input type="submit" value="Add Memo">
    </form>
    
    <hr>
    
    <h2>Current Memo List ({{ memo_list|length }} items)</h2>
    <ul>
        {% for memo in memo_list %}
            <li>{{ memo }}</li>
        {% endfor %}
    </ul>
{% endblock %}
```

#### 3\. `templates/base.html` (Connecting Flash Messages and Static Files)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Day 5 Mission</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <header>...</header>

    {% with messages = get_flashed_messages(with_categories=true) %}
        {% if messages %}
            <div class="flash-messages">
                {% for category, message in messages %}
                    <div class="alert alert-{{ category }}">{{ message }}</div>
                {% endfor %}
            </div>
        {% endif %}
    {% endwith %}

    <main>{% block content %}{% endblock %}</main>
    <footer>...</footer>
</body>
</html>
```

### 🎯 Deconstruction Learning Guide

  * **PRG Verification:** Verify that the address bar remains clean at `http://127.0.0.1:5000/` after adding a memo, and confirm that refreshing the page **does not** result in duplicate data being added.
  * **Flash Messages:** Understand the session-based, one-time storage principle behind why the message is displayed **exactly once** and disappears upon refresh.
  * **`url_for`:** Although you could use `/` directly instead of `home` in `redirect(url_for('home'))`, consider **why using the function name is better for maintainability**.

-----
