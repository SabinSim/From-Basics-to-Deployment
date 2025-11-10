# Day 2 Mission: Implementing Multi-Page Functionality Using Routing

## 💡 Core Problem Identification

> **[Problem]** Our website will have **multiple different addresses**—such as an About page (`/about`) and a Contact page (`/contact`)—in addition to the Home page (`/`). How can the server dynamically show users **different content (different HTML/text)** depending on the requested address?

## 🛠️ Targeted Goal

1.  Understand the extended usage of Flask **Routing (@app.route)**.
2.  Define **multiple View Functions** within a single Flask application.
3.  Implement a minimal web app that outputs **different responses** when accessing different URLs.

-----

## 🔑 Key Learning: Routing Extension

**Routing** is the process of connecting a requested URL path to a specific Python function (the View Function). While Day 1 only covered the `/` path, we now structure the website by defining multiple routes.

  * **Multiple `@app.route` Decorators:** Flask allows you to use the `@app.route` decorator multiple times to map **different URLs** to **different View Functions**.
  * **View Function Independence:** Each View Function only responds to its assigned URL request and operates independently without interfering with others.

-----

## 💻 Completed Solution Code (Day 2 Daily Goal)

The `app.py` code below handles three different URLs (`/, /about, /contact`) and returns a unique content response for each connection.

### `app.py`

```python
# 1. Import the Flask module, necessary for creating the web server.
from flask import Flask

# 2. Create the Flask application object. This variable (app) manages the entire server.
app = Flask(__name__)

# =========================================================
# 3. Multi-Routing: Connecting View Functions to Each URL
# =========================================================

# A. Home Page Routing: This function executes when a user accesses 'http://...:5000/'.
@app.route('/', methods=['GET'])
def home():
    # This function handles the homepage request and returns a welcome message.
    return '<h1>Home Page</h1><p>This is the main page of the web app. Day 2 Mission Success!</p>'

# B. About Page Routing: This function executes when a user accesses 'http://...:5000/about'.
@app.route('/about', methods=['GET'])
def about():
    # This function handles the about page request and returns company/team introduction.
    return '<h1>About Us</h1><p>We grow through Problem-Based Learning (PBL).</p>'

# C. Contact Page Routing: This function executes when a user accesses 'http://...:5000/contact'.
@app.route('/contact', methods=['GET'])
def contact():
    # This function handles the contact page request and returns contact information.
    return '<h1>Contact</h1><p>For inquiries, please send an email to contact@pbl.com.</p>'

# =========================================================
# 4. Server Startup
# =========================================================

if __name__ == '__main__':
    # Starts the server and begins listening for requests.
    # debug=True ensures the server automatically restarts whenever the code is changed.
    app.run(debug=True)
```

### How to Run

1.  Save the code in an **`app.py`** file.
2.  Run the server in your terminal: `python app.py`
3.  Verify the **different content** by accessing the following three addresses in your browser:
      * `http://127.0.0.1:5000/`
      * `http://127.0.0.1:5000/about`
      * `http://127.0.0.1:5000/contact`

-----

## 🎯 Day 2 Mission Completion and Deconstruction Learning

### 1\. Deconstructing the Code

  * **Relationship between `@app.route` and Function Name:** Check if routing still works even if you change the names of the view functions (e.g., `home`, `about`). Flask locates the function solely based on the **path in the `@app.route` decorator**.
  * **Understanding the 404 Error:** Access an address that is not defined in the routing rules (e.g., `/mission`) and observe the **`404 Not Found`** message in your browser. It's crucial to understand how the server handles undefined requests.
  * **URL Design:** Consider how to structure your website's addresses (`/about`, `/contact`) to be intuitive for the user. This forms the foundation of **RESTful API** design.

-----

