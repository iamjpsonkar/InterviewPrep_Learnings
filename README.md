[DOC links](https://github.com/DopplerHQ/awesome-interview-questions)

# Python Programming

## Syntax and Basics

### Variables and Data Types

```python
# Variables
name = "John"
age = 25
is_student = False

# Common Data Types
integer_number = 42
float_number = 3.14
text = "Hello, World!"
list_example = [1, 2, 3]
dictionary_example = {"key": "value"}
```

### Operators and Expressions

```python
# Arithmetic Operators
result = 10 + 5
remainder = 10 % 3

# Comparison Operators
is_equal = (5 == 5)
not_equal = (5 != 3)

# Logical Operators
logical_and = (True and False)
logical_or = (True or False)

# Expressions
expression_result = (2 * (3 + 4)) / 2
```

## Advanced Python

### List Comprehensions
```python
squares = [x**2 for x in range(10)]
```

### Generators
```python
generator_example = (x for x in range(10))

# Access values using next()
first_value = next(generator_example)
second_value = next(generator_example)

print("First Value:", first_value)
print("Second Value:", second_value)
```

### Decorators
```python
def wrapper(func,*args,**kwargs):
    def inner(*args, **kwargs):
        print("before function call")
        return_values = func(*args,**kwargs)
        print("after function call")
        return return_values
    return inner

@wrapper
def myfun(a,b,c):
    print("printing ",a,b,c)
    return a+b,b+c

myfun(a=1,b=2,c=3)
```

### Exception Handling
```python
try:
    result = 10 / 0
except ZeroDivisionError:
    result = "Cannot divide by zero"
```

### Context Managers
```python
with open("example.txt", "r") as file:
    content = file.read()
```

### Closures Functions
```python
def outer_function(x):
    def inner_function(y):
        return x + y
    return inner_function

closure_example = outer_function(10)
closure_result = closure_example(5)
print(closure_result)
closure_result = closure_example(closure_result)
print(closure_result)
```

### Lambda Functions 
```python
square = lambda x: x**2
```

### Concurrency and Parallelism [No IDEA]
```python
import concurrent.futures

# Concurrency with Threads
def print_numbers():
    for i in range(5):
        print(i)

with concurrent.futures.ThreadPoolExecutor() as executor:
    executor.submit(print_numbers)

# Parallelism with Processes
with concurrent.futures.ProcessPoolExecutor() as executor:
    executor.submit(print_numbers)
```

# Backend Development

## API Development

### RESTful Principles:
- **REST (Representational State Transfer)** is an architectural style for designing networked applications.
- Key principles include stateless communication, resource identification, and uniform interfaces.

### CRUD Operations:
- CRUD stands for Create, Read, Update, and Delete, representing the basic operations for persistent storage.
- [PrepDoc](https://github.com/iamjpsonkar/CRUD_Learnings/blob/main/README.md)
###  Authentication and Authorization:
- Authentication ensures that a user is who they claim to be.
- Authorization determines the level of access a user has.
- [Authentication and Authorization Document](https://github.com/iamjpsonkar/CRUD_Learnings/blob/main/README.md#authentication-and-authorization)

## Optimization Techniques

### Database Indexing:
- Indexes improve the speed of data retrieval operations on a database table.
- Common types include B-tree, hash, and full-text indexes.
### Caching Strategies:
- Caching involves storing copies of files or data in a location to serve future requests faster.
- Techniques include in-memory caching, CDN caching, and browser caching.
### Load Balancing:
- Load balancing distributes incoming network traffic across multiple servers to ensure no single server is overwhelmed.

## Transaction Management

### ACID Properties:
- ACID stands for Atomicity, Consistency, Isolation, and Durability, ensuring reliable database transactions.
### Isolation Levels:
- Isolation levels define the degree to which one transaction must be isolated from the effects of others.

## Security Best Practices
### Input Validation:
- Validate and sanitize user input to prevent security vulnerabilities.
### XSS and CSRF Prevention:
- Cross-Site Scripting (XSS) and Cross-Site Request Forgery (CSRF) are common web application security vulnerabilities.

# Web Frameworks

## Flask

### Routing and Views
*Routing is the process of mapping URLs to functions in your Flask application. Views are the functions that handle the requests and generate responses.*

```python
from flask import Flask

app = Flask(__name__)

# Define a route
@app.route('/')
def home():
    return 'Hello, this is the home page!'

# Another route
@app.route('/about')
def about():
    return 'This is the about page.'

if __name__ == '__main__':
    app.run(debug=True)
```

### Templates and Forms
*Templates allow you to render dynamic content, and forms help manage user input.*
```python
from flask import Flask, render_template, request

app = Flask(__name__)

# Render HTML template
@app.route('/')
def home():
    return render_template('home.html')

# Handle form submission
@app.route('/submit', methods=['POST'])
def submit():
    if request.method == 'POST':
        username = request.form.get('username')
        return f'Hello, {username}!'

if __name__ == '__main__':
    app.run(debug=True)
```


### Flask Extensions
*Flask extensions enhance the functionality of your application. Here's an example using Flask-WTF for form handling.*

```python
from flask import Flask, render_template
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your_secret_key'

# Define a form using Flask-WTF
class MyForm(FlaskForm):
    username = StringField('Username')
    submit = SubmitField('Submit')

# Route using the form
@app.route('/form', methods=['GET', 'POST'])
def form():
    form = MyForm()
    if form.validate_on_submit():
        username = form.username.data
        return f'Form submitted with username: {username}'
    return render_template('form.html', form=form)

if __name__ == '__main__':
    app.run(debug=True)
```

`pip install Flask Flask-WTF`

## Django
[Django](https://github.com/iamjpsonkar/Django_learnings/blob/main/README.md)

## Sanic
### **Not Covering in Deep**

### Asynchronous Request Handlers
*Sanic supports asynchronous request handlers, allowing you to write non-blocking, asynchronous code for improved performance.*

```python
from sanic import Sanic
from sanic.response import text

app = Sanic()

# Asynchronous request handler
@app.route('/')
async def home(request):
    return text('Hello, this is the home page!')

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000, debug=True, workers=4)
```

### Middleware
*Middleware in Sanic allows you to process requests globally, providing a way to modify or handle requests before they reach the route handler.*

```python
from sanic import Sanic
from sanic.response import text

app = Sanic()

# Middleware example
async def custom_middleware(request):
    print("This is executed for every request before reaching the route handler.")
    return await request.next()

app.register_middleware(custom_middleware)

# Route handler
@app.route('/')
async def home(request):
    return text('Hello, this is the home page!')

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000, debug=True, workers=4)
```

### Blueprints
*Blueprints in Sanic help modularize your application by grouping related routes.*

```python
from sanic import Sanic
from sanic import Blueprint
from sanic.response import text

app = Sanic()

# Create a blueprint
bp = Blueprint('my_blueprint')

# Route within the blueprint
@bp.route('/blueprint')
async def blueprint_handler(request):
    return text('This is a route in the blueprint.')

# Register the blueprint with the app
app.blueprint(bp)

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000, debug=True, workers=4)
```

# Database Management

## SQL Databases
### SQL Queries, Joins, Aggregations:
- SQL queries retrieve and manipulate data, join and combine data from multiple tables, and aggregate data.
### Indexing and Optimization:
- Indexing involves creating indexes for faster query execution, and optimization ensures efficient database performance.

## NoSQL Databases
### Overview of MongoDB, Redis, etc.:
- NoSQL databases like MongoDB and Redis offer alternatives to traditional relational databases.

### MongoDB
*MongoDB is a NoSQL database that stores data in a flexible, JSON-like format known as BSON (Binary JSON). It is designed to handle large amounts of unstructured or semi-structured data. MongoDB is classified as a document-oriented database, part of the NoSQL family, and is often used in web development as a backend database for applications.*

#### Key Concepts
- **Document**: A document is a basic unit of data in MongoDB, and it is a set of key-value pairs. Documents are similar to JSON objects and can contain arrays and other documents.
    ```js
    {
        "_id": ObjectId("5fd7a7c2b4ae240d08f00b5a"),
        "name": "John Doe",
        "age": 30,
        "email": "john.doe@example.com",
        "address": {
            "city": "New York",
            "state": "NY",
            "country": "USA"
        }
    }
    ```

- **Collection**: A collection is a grouping of MongoDB documents. It is equivalent to an RDBMS table. Collections don't enforce a schema, meaning documents within a collection can have different fields.

- **Database**: MongoDB stores collections in databases. A single MongoDB server can host multiple databases, each with its own set of collections.

#### Basic MongoDB Queries

- Insert a Document
```js
db.users.insertOne({
    "name": "Jane Doe",
    "age": 25,
    "email": "jane.doe@example.com",
    "address": {
        "city": "Los Angeles",
        "state": "CA",
        "country": "USA"
    }
})
```

- Find Documents
```js
// Find all documents in the 'users' collection
db.users.find()

// Find documents with a specific condition
db.users.find({"age": {"$gt": 25}})
```

- Update Document
```js
// Update a document
db.users.updateOne(
    {"name": "John Doe"},
    {"$set": {"age": 31}}
)
```

- Delete Document
```js
// Delete a document
db.users.deleteOne({"name": "Jane Doe"})
```

- Aggregation
```js
// Aggregate data (e.g., group by and calculate average)
db.users.aggregate([
    {"$group": {"_id": "$address.city", "average_age": {"$avg": "$age"}}}
])
```

#### PyMongo
```python
from pymongo import MongoClient

# Connect to MongoDB
client = MongoClient("mongodb://localhost:27017/")  # Update with your MongoDB connection string
database_name = "example_db"
collection_name = "users"

db = client[database_name]
collection = db[collection_name]

# Create Index (optional)
collection.create_index("email", unique=True)

# Insert Documents
data_to_insert = [
    {
        "name": "John Doe",
        "age": 30,
        "email": "john.doe@example.com",
        "address": {
            "city": "New York",
            "state": "NY",
            "country": "USA"
        }
    },
    {
        "name": "Jane Doe",
        "age": 25,
        "email": "jane.doe@example.com",
        "address": {
            "city": "Los Angeles",
            "state": "CA",
            "country": "USA"
        }
    }
]

# Insert multiple documents
collection.insert_many(data_to_insert)

# Find Documents
all_users = collection.find()

for user in all_users:
    print(user)

# Query with a condition
specific_users = collection.find({"age": {"$gt": 25}})
print("\nUsers older than 25:")
for user in specific_users:
    print(user)

# Update Document
collection.update_one({"name": "John Doe"}, {"$set": {"age": 31}})

# Delete Document
collection.delete_one({"name": "Jane Doe"})

# Close MongoDB Connection
client.close()
```

## Database Design
### Normalization and Denormalization:
- Normalization organizes data to reduce redundancy, while denormalization simplifies data retrieval.
### Entity-Relationship Diagrams (ERD):
- ERDs visualize the relationships between entities in a database.

# DevOps and Tools

## Git

### Concepts

- **Branching, Merging, Resolving Conflicts:**
  - Git allows branching for parallel development.
  - Merging integrates changes.
  - Conflict resolution manages conflicting changes.

- **Gitflow Workflow:**
  - Gitflow is a branching model that defines a strict branching strategy.

### Content for Revision

- Practice creating branches, merging branches, and resolving conflicts in Git.
- Understand the Gitflow workflow for collaborative development.

## Bash Scripting

### Concepts

- **Basic Commands:**
  - Basic Linux commands for navigation, file manipulation, and system interaction.

- **Scripting for Automation:**
  - Writing Bash scripts to automate repetitive tasks.

### Content for Revision

- Review basic Linux commands (cd, ls, cp, mv, rm, mkdir, etc.).
- Practice writing Bash scripts for automating tasks.

## Linux

### Concepts

- **File System Structure:**
  - Understanding the Linux file system hierarchy.

- **Process Management:**
  - Basic process management commands like ps, kill, top.


## Docker

### Concepts

- **Containerization Concepts:**
  - Docker containers encapsulate applications and their dependencies for consistency across different environments.

- **Docker Compose:**
  - Docker Compose simplifies multi-container application management.

# Frontend Development
## Web Development Basics
[Web Development](https://github.com/iamjpsonkar/WebLearnings/blob/main/README.md)
### HTML, CSS, JavaScript
- HTML structures web content, CSS styles it and JavaScript adds interactivity.
### Responsive Design
- Designing websites to be accessible and functional on various devices.


## Node.js
[Node Learnings](https://github.com/iamjpsonkar/Nodejs_Learnings/blob/master/README.md)
### Server-Side JavaScript
- Node.js enables JavaScript to run on the server.
### npm (Node Package Manager)
- npm manages JavaScript packages and dependencies.

### Content for Revision
- Understand the basics of server-side JavaScript with Node.js.
- Explore npm commands for package management.

# AI/ML Development
[AI/ML Development](https://github.com/iamjpsonkar/ML_Learnings/blob/master/README.md)

## Machine Learning Concepts

### Supervised and Unsupervised Learning
- Supervised learning uses labeled data, unsupervised learning works with unlabeled data.

### Regression, Classification, Clustering
- Different types of machine learning tasks.

## Data Science Basics

### Data Cleaning, Exploration, Visualization
- Preparing and exploring data before analysis.

### Statistical Concepts
- Understanding statistical measures and distributions.

## Python for AI/ML

### Libraries (NumPy, Pandas, Matplotlib, Scikit-learn)
- Essential Python libraries for AI/ML tasks.

### Jupyter Notebooks
- Interactive computing for data analysis.

# Data Structures and Algorithms
[String Algorithms](https://github.com/iamjpsonkar/Algorithm_learnings/blob/main/README.md)
[Data Structure and Algorithms](https://github.com/iamjpsonkar/DS_ALGO/blob/main/README.md)

# System Design
[System Design](https://github.com/iamjpsonkar/SystemDesign_Learnings/blob/master/README.md)

