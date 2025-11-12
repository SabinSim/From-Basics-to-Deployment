# Day 4 Mission: Dynamic Multi-Page Rendering with Templates

## 💡 Core Problem Identification

> **[Problem]** Writing HTML directly inside Python strings is inefficient, and we are forced to repeat **common structural elements** like headers and footers on every page. How can we **reuse repetitive HTML structures** and **neatly inject** server data into the HTML to create dynamic pages?

## 🛠️ Targeted Goal

1.  Use Flask's **`render_template`** function to load HTML files.
2.  Understand the basic syntax of the **Jinja2 Template Engine** (`{{ }}` and `{% for %}`).
3.  Reuse a common layout using **Template Inheritance (`{% extends %}`)**.

## 🔑 Key Learning: The Jinja2 Template Engine

  * **Template Separation:** Flask recommends creating a `templates` folder and managing HTML files separately within it.
  * **`render_template`:** This function is responsible for injecting data prepared in the server logic (Python) into the HTML template, and then delivering the final HTML file to the client.
  * **Jinja2 Syntax:**
      * **`{{ variable }}`:** Used to output data passed from the server.
      * **`{% control_statement %}`:** Used to execute logic like `for` loops or `if` conditions directly within the HTML.

**💡 Environment Setup:** For this mission, you must create a folder named **`templates`** in the same directory as `app.py` and save `base.html` and `index.html` inside it.

### 💻 Completed Solution Code (File Separation)

#### 1\. `app.py` (Flask Server File)

```python
# 1. Import Flask and the render_template function for template rendering.
from flask import Flask, render_template

# 2. Create the Flask application object.
app = Flask(__name__)

# 3. Routing: Prepares data and renders the template upon a homepage request.
@app.route('/', methods=['GET'])
def index():
    # Prepare the data to be shown on the web page (simulating real DB data).
    todos = [
        {'id': 1, 'task': 'Review HTTP Principles'},
        {'id': 2, 'task': 'Practice Routing'},
        {'id': 3, 'task': 'Master Jinja2 Templates (Today\'s Mission!)'}
    ]
    page_title = 'PBL Day 4: Dynamic Templates'
    
    # Use render_template() to render 'templates/index.html' and pass the 
    # todos and title data to the template.
    return render_template('index.html', title=page_title, todo_list=todos)

# 4. Server Startup
if __name__ == '__main__':
    app.run(debug=True)
```

#### 2\. `templates/base.html` (Common Layout File)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!-- Jinja2: Use the passed 'title' variable -->
    <title>{{ title }} - PBL Project</title>
</head>
<body>
    <header>
        <h1>Main PBL Web App</h1>
        <nav>
            <a href="/">Home</a> |
            <a href="/about">About</a> 
        </nav>
    </header>

    <main>
        <!-- Jinja2: This block is where child templates will insert their unique content. -->
        {% block content %}{% endblock %}
    </main>

    <footer>
        <p>&copy; 2025 PBL Learning Project.</p>
    </footer>
</body>
</html>
```

#### 3\. `templates/index.html` (Main Page File)

```html
<!-- Jinja2: Inherit the layout from the base.html file -->
{% extends 'base.html' %}

<!-- Jinja2: Define the content that will be inserted into the 'content' block in base.html -->
{% block content %}
    <h1>{{ title }}</h1>
    
    <h2>Todo List</h2>
    <ul>
        <!-- Jinja2: Loop through the 'todo_list' data passed from the server -->
        {% for todo in todo_list %}
            <li>
                <!-- Jinja2: loop.index provides the current iteration number -->
                <strong>{{ loop.index }}.</strong> {{ todo.task }} 
            </li>
        {% endfor %}
        </ul>
{% endblock %}
```

### 🎯 Deconstruction Learning Guide

  * **Template Inheritance:** Understand why the header and footer appear on the screen even though the `index.html` file does not contain their code, by grasping the relationship between `extends` and `block`.
  * **Data Flow Visualization:** Visualize the sequence of data flow: `app.py` -\> `render_template` arguments -\> `{{ }}` variables in `index.html`.

