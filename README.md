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

