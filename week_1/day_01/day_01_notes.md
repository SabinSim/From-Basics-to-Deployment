

# Day 1 Mission: Understanding and Implementing the Foundation of Web Communication

## 💡 Core Problem Identification

> **[Problem]** When a web browser (client) enters a URL like `https://www.google.com` into the address bar, **what happens internally**, and how can we build the foundation for a server to respond with a **Static Page**?

## 🛠️ Targeted Goal

1.  Understand the **principles of HTTP communication (Request/Response)**.
2.  Understand the role of the `GET` method.
3.  Set up **Flask** and implement a minimal server that **responds with static content**.

-----

## 🔑 Key Learning: The First Encounter with HTTP and Flask

### 1\. HTTP Fundamentals: The Request-Response Cycle

The web fundamentally operates on a **client (browser) sending a request** and a **server sending a response**.

| **Entity** | **Action** | **Description** |
| :--- | :--- | :--- |
| **Client** (Browser) | **Request** | Sends the URL, HTTP method (GET, POST, etc.), headers, and data to the server. |
| **Server** (Flask Application) | **Response** | Processes the request and returns the result (HTML, JSON, etc.), HTTP Status Code, and headers to the client. |

  * **GET Method:** The most basic method used for **retrieving (Reading)** data.

### 2\. HTTP Status Codes

These are standardized numerical codes the server uses to tell the client the result of the request processing.

  * **`200 OK`**: The request was successful. (The most common successful response.)
  * **`404 Not Found`**: The requested resource (URL) could not be found.
  * **`500 Internal Server Error`**: An error occurred within the server. (An error frequently encountered during development.)

### 3\. Flask Environment Setup and Basic Structure

Flask is a **micro web framework** based on Python.

  * **Installation:** `pip install Flask`
  * **Most Basic Structure:**
      * The core application is created by instantiating the **`Flask` object**.
      * A **decorator** like `@app.route('/')` is used to map a specific URL (route) to a corresponding function (**View Function**) that will handle the request.

-----

## 💻 Completed Solution Code (Day 1 Daily Goal)

The code below represents the minimal Flask server structure that returns a static "Hello, World\!" response when a web browser connects to it.

First, save the following code as **`app.py`** and run it.

### `app.py`

```python
# 1. Import the Flask module.
from flask import Flask

# 2. Create the Flask application object.
# __name__ is the name of the current module, which Flask uses to locate resources.
app = Flask(__name__)

# 3. Routing: Define a view function to handle requests to the base URL ('/').
# '@app.route('/')' tells Flask to execute the 'hello_world' function below
# when the web browser sends a GET request to 'http://127.0.0.1:5000/'.
@app.route('/', methods=['GET'])
def hello_world():
    # 4. The function returns the 'Response' to be sent back to the client.
    # This response becomes the body of the HTTP Response.
    return '<h1>Hello, PBL World!</h1><p>This is the server\'s response.</p>'

# 5. Configure the server to run only when the file is executed directly.
if __name__ == '__main__':
    # Setting debug mode to True enables the server to automatically restart upon code changes. (Convenient during development)
    app.run(debug=True)
```

### How to Run

1.  **Set up Virtual Environment and Install Flask** (If you haven't already):

    ```bash
    # Create a virtual environment
    python -m venv venv
    # Activate the virtual environment (Windows)
    .\venv\Scripts\activate
    # Activate the virtual environment (Mac/Linux)
    source venv/bin/activate

    # Install Flask
    pip install Flask
    ```

2.  **Run the Server:**

    ```bash
    python app.py
    ```

3.  **Verify the Result:** Enter the address displayed in your terminal (`http://127.0.0.1:5000/`) into your web browser and connect.

-----

## 🎯 Day 1 Mission Completion and Deconstruction Learning

### 1\. Deconstructing the Code

  * Examine **why** `from flask import Flask` is necessary and which functionality (class) is being imported from the Flask module.
  * Think about the reason for explicitly specifying `GET` in **`@app.route('/', methods=['GET'])`** by connecting it to the **HTTP methods** concept. (What error would occur if you changed it to `methods=['POST']` and tried to access it through a browser? - *It is crucial to try this yourself\!*)
  * Connect the concept of the **HTTP Response body** to understand why the `hello_world` function **returning a string** appears as HTML code to the client (browser).

