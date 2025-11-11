# Day 3 Mission: Implementing Data Submission and Server Processing

## 💡 Core Problem Identification

> **[Problem]** Up until now, the server only displayed data unilaterally. However, real web applications require users to **input data** for things like user registration or commenting. How can we transmit user-entered data to the server, and how does the server **receive and process** it?

## 🛠️ Targeted Goal

1.  Understand and utilize the **POST method**.
2.  Understand the principle of data transmission using the HTML **`<form>` tag**.
3.  Use Flask's **`request` object** to receive data from the client.

-----

## 🔑 Key Learning: Forms and POST Requests

  * **POST Method:** Used to **create** or **update** new data. The data is transmitted within the **Request Body**, hidden from the URL, which makes it generally more secure than GET.
  * **HTML Form:** In `<form method="POST" action="/">`, `method="POST"` instructs the browser to send data using the POST method, and `action="/"` specifies that the data should be sent to the current address.
  * **`request.form`:** Used in Flask to access **form data** sent via POST. The `name` attribute value of the HTML `<input>` tag becomes the **Key** in the dictionary-like `request.form` object.

### 💻 Completed Solution Code (`app.py`)

```python
# 1. Import Flask and the 'request' object, which holds request-specific information.
from flask import Flask, request

# 2. Create the Flask application object.
app = Flask(__name__)

# =========================================================
# 3. Handle both GET (form display) and POST (data processing) for form data reception.
# =========================================================

# This function handles both GET and POST requests to the '/' address.
@app.route('/', methods=['GET', 'POST'])
def handle_message():
    
    # 3-1. When the client first requests the page (GET Request)
    if request.method == 'GET':
        # Respond with an HTML form where the user can input a message.
        # Note the method="POST" and action="/" attributes in the <form> tag.
        return '''
            <h1>Day 3 Mission: Message Submission</h1>
            <form method="POST" action="/">
                <label for="user_message">Enter Message:</label><br>
                <input type="text" id="user_message" name="user_message" required><br><br>
                <input type="submit" value="Send to Server">
            </form>
        '''

    # 3-2. When the user submits the form (POST Request)
    elif request.method == 'POST':
        # Safely retrieve the form data ('user_message') using request.form.get().
        message = request.form.get('user_message')
        
        # Print the received data to the server console to prove processing.
        print("------------------------------------------")
        print(f"✅ Message received from client: {message}")
        print("------------------------------------------")
        
        # Return a success response to the client.
        return f'<h1>Success!</h1><p>Your message "{message}" has arrived at the server.</p>'

# 4. Server Startup
if __name__ == '__main__':
    app.run(debug=True)
```

### 🎯 Deconstruction Learning Guide

  * **GET vs. POST Branching:** You must fully understand the structure of handling GET and POST separately within a single View Function using `request.method`. This is fundamental to implementing **CRUD** (Create, Read, Update, Delete) operations.
  * **Data Key Matching:** Verify that the `name` attribute value in the HTML `<input name="XXX">` matches the key value in Python's `request.form.get('XXX')`.

-----
