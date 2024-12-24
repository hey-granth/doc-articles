# Notes

So I don't forget the stuff I learn here.

---
## UserMixIn
It is a class in flask-login module which provides the following methods:
- `is_authenticated()`: Returns True if the user is authenticated.
- `is_active()`: Returns True if the user is active.
- `is_anonymous()`: Returns True if the user is an anonymous user.
- `get_id()`: Returns the unique identifier for the user.

---
## Bcrypt
bcrypt is a hashing library in python, which hashes the passwords so that they can be stored more securely
in the database. It is used to hash the passwords before storing them in the database and to compare the
hashed passwords when the user logs in.

Even if the data is compromised, the passwords are still secure because the hacker would have to decrypt it,
which is too difficult to do, unless you have the actual passwords.

---
## Difference Between Module and Library in Python

|  **Feature**   |          **Module**          |           **Library**            |
|:--------------:|:----------------------------:|:--------------------------------:|
| **Definition** |     A single `.py` file.     |     A collection of modules.     |
|   **Scope**    |    Small, specific tasks.    |      Broader functionality.      |
|  **Examples**  |         `math`, `os`         |   `NumPy`, `Pandas`, `Flask`.    |
|   **Usage**    |     `import module_name`     |`import library_name.module_name` |


### **Module**


A module is a single Python file containing code like functions, classes, or variables.

#### Example:
```python
# my_module.py
def greet(name):
    return f"Hello, {name}!"

import my_module
print(my_module.greet("Alice"))  # Output: Hello, Alice!
```
---
## Decorators

Decorators in Python are functions that modify the behavior of another function or method. They allow you to "wrap" another function to add functionality without changing its structure.

### How Decorators Work
- A decorator takes a function as input, adds some functionality, and returns a new function.
- You use the `@decorator_name` syntax to apply a decorator to a function.

### Example Without Using `@` Syntax
```python
def decorator(func):
    def wrapper():
        print("Before the function call")
        func()
        print("After the function call")
    return wrapper

def say_hello():
    print("Hello!")

decorated_function = decorator(say_hello)
decorated_function()
```
---
## Modals
Modals are dialog boxes or pop-ups that appear on top of the current page. They are used to display information, ask for user input, or confirm an action.
![img.png](modal.png)
---
## Pagination
### What is Pagination?
Pagination is a technique used to divide content into separate pages, allowing users to navigate through large sets of data in smaller, more manageable chunks. Think of it like chapters in a book or pages in a magazine – instead of showing everything at once, the content is broken down into discrete pages.
### Why Use Pagination?
When dealing with large datasets, pagination offers several important benefits:

- **Performance Optimization**: Rather than loading thousands of records at once, pagination lets servers send only a small portion of data at a time, significantly improving load times and reducing server strain.
- **Better User Experience**: Users can easily navigate through content without being overwhelmed by endless scrolling or massive data dumps. This is particularly important when displaying search results, blog posts, or product listings.
---
## What is `itsdangerous` in Python?

`itsdangerous` is a Python library that helps you securely handle untrusted data by providing cryptographic signing and verification. It is often used to protect data like session cookies, tokens, or other sensitive information.

### Key Features
- **Signing Data**: Ensures that data has not been tampered with.
- **Timed Tokens**: Allows you to create tokens that expire after a set time.
- **Compact and Lightweight**: Easy to integrate into projects.

### Why Use `itsdangerous`?
When working with web applications, you may need to send data to the client (like a token or session ID) and later verify that the data was not modified. `itsdangerous` ensures this by signing the data with a secret key.

### Example Usage
Here’s a simple example:

```python
from itsdangerous import URLSafeSerializer

# Create a serializer with a secret key
serializer = URLSafeSerializer("my-secret-key")

# Sign some data
data = {"user_id": 123}
signed_data = serializer.dumps(data)
print("Signed Data:", signed_data)

# Verify and load the signed data
try:
    original_data = serializer.loads(signed_data)
    print("Original Data:", original_data)
except Exception as e:
    print("Invalid or tampered data!", e)
```

### Common Use Cases
- Generating secure tokens for password reset links.
- Signing session data for web applications.
- Protecting API payloads.

### Installation
Install `itsdangerous` using pip:

```bash
pip install itsdangerous
```

### Additional Resources
- [Official Documentation](https://itsdangerous.palletsprojects.com/)
- [GitHub Repository](https://github.com/pallets/itsdangerous)
---
## Static Methods in Python

A **static method** is a method that belongs to a class, not an instance of the class. It does not require access to instance (`self`) or class (`cls`) attributes or methods. Static methods are defined using the `@staticmethod` decorator.

### Key Points
- **No `self` or `cls`**: Static methods don’t take instance or class references as their first parameter.
- **Independent**: They are like regular functions but grouped within a class for better organization.
- **Access**: Can be called using the class name or an instance.

### When to Use
Use static methods for utility or helper functions that don’t depend on the class or instance but are conceptually related to the class.

### Example
```python
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b

# Access via the class
result1 = MathUtils.add(5, 3)
print("Result1:", result1)  # Output: 8

# Access via an instance
utils = MathUtils()
result2 = utils.add(10, 7)
print("Result2:", result2)  # Output: 17
```

### Summary
Static methods are useful for grouping related functions within a class without relying on instance or class-specific data. Use `@staticmethod` to define them.

---
## Transport Layer Security

Transport Layer Security (TLS) is a cryptographic protocol that ensures secure communication over a network. It provides:

- **Encryption**: Protects data from being read by unauthorized parties.
- **Authentication**: Verifies the identity of communicating parties.
- **Integrity**: Ensures data is not altered during transmission.

TLS is widely used in web browsers, email, messaging, and other applications to protect sensitive information like passwords and credit card details. It is the successor to Secure Sockets Layer (SSL).

---
## Flask Blueprints: A Beginner-Friendly Explanation

Flask Blueprints are a way to organize and structure a Flask application into smaller, reusable components. They allow you to split your app into multiple modules, making it easier to manage, especially as your project grows.

### Why Use Blueprints?
- **Modular Code**: Helps keep your application code clean and organized.
- **Reusability**: You can reuse blueprints across different projects.in]
  git add ./
  ~/WebstormProjects/doc-articles git:[main]
  git commit -m "added flask notes"
  [main 8a82b5c] added flask notes
  2 files changed, 248 insertions(+)
  create mode 100644 src/pages/flask.md
  create mode 100644 src/pages/modal.png
- **Collaboration**: Makes it easier for multiple developers to work on different parts of the app.

### How Do Blueprints Work?
A blueprint is like a mini Flask application that can define routes, views, templates, and static files. Once defined, it is registered with the main Flask app.

### Basic Example
Here’s how to use Flask Blueprints:

#### Step 1: Create a Blueprint
Create a new file, e.g., `routes.py`:

```python
from flask import Blueprint

# Define a blueprint
main = Blueprint('main', __name__)

@main.route('/')
def home():
    return "Welcome to the Home Page!"

@main.route('/about')
def about():
    return "About Page"
```

#### Step 2: Register the Blueprint
In your main application file (e.g., `app.py`):

```python
from flask import Flask
from routes import main  # Import the blueprint

app = Flask(__name__)

# Register the blueprint
app.register_blueprint(main)

if __name__ == '__main__':
    app.run(debug=True)
```

#### Step 3: Run the App
When you run `app.py`, the routes defined in the blueprint will be accessible.

### Key Points
- Blueprints help organize large Flask applications.
- You can define multiple blueprints for different parts of your app (e.g., user authentication, admin panel).
- Blueprints can have their own templates and static files.

Using Flask Blueprints is a great way to keep your app maintainable and scalable!

---
## Common HTTP Errors

### 404: Not Found
The server couldn't find the requested resource. This typically occurs when the URL is incorrect or the resource has been moved or deleted.

### 403: Forbidden
The server understands the request but refuses to authorize it. This often happens when access permissions are insufficient.

### 500: Internal Server Error
The server encountered an unexpected condition that prevented it from fulfilling the request. This is usually caused by a server-side issue or bug.

---
