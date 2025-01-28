## Introduction to Python

Python is a popular, easy-to-learn programming language used in many fields, including web development, data science, and automation. Python has a simple syntax that makes it beginner-friendly, yet it is powerful enough for professional development.

## How to Install Python and Run Python Code

To install Python, follow these steps:

- Visit [python.org](https://www.python.org/downloads/) and download the latest version of Python.
- During installation, ensure the checkbox **"Add Python to PATH"** is checked.

To run Python code:
- Open the terminal or command prompt.
- Type `python` to start the Python interactive shell (REPL).
- Alternatively, you can save Python scripts in files with the `.py` extension and run them from the terminal using `python filename.py`.

### Example Code

You can test your installation by typing this code in Python:

```python
print("Hello, World!")
```

__Expected Output__

```
Hello, World!
```

## Types of Variables

Variables in Python are used to store data values. The variable name can be anything (as long as it follows naming rules), and the type of the variable is inferred based on the value assigned to it.

### Example

```python
x = 5       # Integer
y = 3.14    # Float
name = "John"  # String
is_active = True  # Boolean
```

__Output__

```python
print(type(x))  # <class 'int'>
print(type(y))  # <class 'float'>
print(type(name))  # <class 'str'>
print(type(is_active))  # <class 'bool'>
```

## Types of Data

Python has several built-in data types. Here are some of the most common:

- **int**: Integer numbers (e.g., 1, 100, -5)
- **float**: Floating-point numbers (e.g., 3.14, 1.0, -0.1)
- **str**: String (text) values (e.g., "hello", "world")
- **bool**: Boolean values (`True` or `False`)
- **list**: Ordered collection of items (e.g., `[1, 2, 3]`)
- **tuple**: Immutable ordered collection (e.g., `(1, 2, 3)`)
- **dict**: Collection of key-value pairs (e.g., `{"name": "John", "age": 30}`)

### Example

```python
my_list = [1, 2, 3, 4]
my_tuple = (5, 6, 7)
my_dict = {"name": "John", "age": 30}

print(type(my_list))  # <class 'list'>
print(type(my_tuple))  # <class 'tuple'>
print(type(my_dict))  # <class 'dict'>
```

## Mathematical Operations

Python can handle basic mathematical operations:

- Addition (`+`)
- Subtraction (`-`)
- Multiplication (`*`)
- Division (`/`)
- Modulus (remainder) (`%`)
- Exponentiation (`**`)
- Floor Division (`//`)

### Example

```python
a = 10
b = 3

print(a + b)  # Addition
print(a - b)  # Subtraction
print(a * b)  # Multiplication
print(a / b)  # Division
print(a % b)  # Modulus
print(a ** b)  # Exponentiation
print(a // b)  # Floor Division
```

__Output__

```
13
7
30
3.3333333333333335
1
1000
3
```

## Conditional Statements (If and Else)

Conditional statements allow us to execute code based on certain conditions using `if`, `elif`, and `else`.

### Example

```python
age = 18

if age >= 18:
    print("You are an adult.")
else:
    print("You are a minor.")
```

__Output__

```
You are an adult.
```

## Looping (For and While)

Loops allow us to repeat a block of code multiple times.

### For Loop

Used to iterate over a sequence (like a list or range).

### Example

```python
for i in range(5):
    print(i)
```

__Output__

```
0
1
2
3
4
```

### While Loop

Repeats as long as a condition is `True`.

### Example

```python
count = 0
while count < 5:
    print(count)
    count += 1
```

__Output__

```
0
1
2
3
4
```

## Functions

Functions are blocks of reusable code that perform a specific task.

### Example

```python
def greet(name):
    print("Hello, " + name + "!")

greet("Alice")  # Calling the function
```

__Output__

```
Hello, Alice!
```

