---
title: python-practices
date: 2024-12-06T10:40:33
categories: [General]
tags: []
---
Here’s a comprehensive breakdown of the approaches, with examples for each **good practice**, and finally, a **cheat sheet** to summarize the good practices for quick reference.

---

### **Good Practices with Examples**

#### **1. Avoid Using Mutable Default Arguments**
Using mutable types like lists, dictionaries, or sets as default arguments can lead to unexpected behavior because the default value is shared across all calls to the function.

**Bad Example:**
```python
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item(1))  # Output: [1]
print(add_item(2))  # Output: [1, 2] (unexpected behavior)
```

**Good Example:**
Use `None` as a default and initialize inside the function:
```python
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items

print(add_item(1))  # Output: [1]
print(add_item(2))  # Output: [2]
```

---

#### **2. Encapsulate Logic in Helper Functions**
Encapsulating logic in helper functions improves readability, avoids redundancy, and keeps initialization separate from core functionality.

**Before Refactoring (Less Readable):**
```python
def generate_all_lists(grid, i=None, taken_list=None):
    if i is None:
        i = 0
        taken_list = []
    if i == len(grid):
        print(taken_list)
        return
    taken_list.append(grid[i])
    generate_all_lists(grid, i + 1, taken_list)
    taken_list.pop()

generate_all_lists([1, 2, 3])
```

**After Refactoring (Encapsulation):**
```python
def generate_all_lists(grid):
    def helper(i, taken_list):
        if i == len(grid):
            print(taken_list)
            return
        taken_list.append(grid[i])
        helper(i + 1, taken_list)
        taken_list.pop()

    helper(0, [])
generate_all_lists([1, 2, 3])
```

---

#### **3. Use List Comprehensions for Independent Lists**
Avoid creating a shared reference between rows in a grid.

**Bad Example:**
```python
grid = [[False] * 3] * 3
grid[0][0] = True
print(grid)  # Output: [[True, False, False], [True, False, False], [True, False, False]]
```

**Good Example:**
```python
grid = [[False for _ in range(3)] for _ in range(3)]
grid[0][0] = True
print(grid)  # Output: [[True, False, False], [False, False, False], [False, False, False]]
```

---

#### **4. Separate Initialization from Core Functionality**
By separating setup/initialization logic into a separate function or section, you make code cleaner and more modular.

**Before (Mixed Logic):**
```python
def process_grid(grid):
    n = len(grid[0])
    taken_grid = [[False] * n for _ in range(len(grid))]
    for row in grid:
        for cell in row:
            print(cell)
```

**After (Separated Initialization):**
```python
def initialize_taken_grid(grid):
    return [[False for _ in row] for row in grid]

def process_grid(grid):
    taken_grid = initialize_taken_grid(grid)
    for row in grid:
        for cell in row:
            print(cell)
```

---

#### **5. Use Iterators/Generators for Efficiency**
When generating large sequences or lists, use iterators or generators instead of precomputing the entire sequence.

**Before (Inefficient Memory Use):**
```python
def generate_numbers(n):
    return [i for i in range(n)]

numbers = generate_numbers(1000000)
print(numbers[:5])
```

**After (Efficient Generator):**
```python
def generate_numbers(n):
    for i in range(n):
        yield i

numbers = generate_numbers(1000000)
print(next(numbers))  # Output: 0
print(next(numbers))  # Output: 1
```

---

#### **6. Use Type Annotations for Clarity**
Type annotations improve code readability and help with debugging.

**Before:**
```python
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
```

**After (With Type Annotations):**
```python
from typing import List, Optional

def add_item(item: int, items: Optional[List[int]] = None) -> List[int]:
    if items is None:
        items = []
    items.append(item)
    return items
```

---

#### **7. Yield Results Instead of Printing**
If the function's results need further processing, use `yield` instead of `print`.

**Before:**
```python
def generate_sequences(sequence):
    print(sequence)
generate_sequences([1, 2, 3])
```

**After:**
```python
def generate_sequences(sequence):
    yield sequence

for seq in generate_sequences([1, 2, 3]):
    print(seq)
```

---

### **Cheat Sheet of Good Practices**

| **Practice**                              | **Good Example**                                                                                   | **Why?**                                          |
|-------------------------------------------|---------------------------------------------------------------------------------------------------|--------------------------------------------------|
| **Avoid mutable default arguments**       | Use `None` as default and initialize inside the function.                                         | Prevents shared state across function calls.     |
| **Encapsulate logic in helpers**          | Use nested functions or separate helpers for recursion or reusable logic.                         | Improves readability and modularity.            |
| **Use independent lists in grids**        | `[[False for _ in range(n)] for _ in range(m)]`                                                   | Prevents shared references.                     |
| **Separate initialization from core logic**| Create a separate function for initialization.                                                    | Keeps code modular and easier to maintain.       |
| **Use generators for efficiency**         | Use `yield` for large data sequences.                                                             | Saves memory by producing items on demand.       |
| **Add type annotations**                  | `def func(x: int) -> str:`                                                                        | Improves readability and debugging.             |
| **Yield results instead of printing**     | Replace `print` with `yield` for better reusability.                                              | Allows further processing of results.           |

---

### **What is `yield`?**

`yield` is a keyword in Python used in **generators**, which are special functions that allow you to generate a sequence of values **lazily** (on demand) instead of creating and storing the entire sequence in memory at once.

When a function contains a `yield` statement, it becomes a **generator function**. Unlike regular functions that return a value and terminate, a generator function can pause execution, yield a value, and resume later from where it paused.

---

### **How `yield` Works**

1. When the generator function is called, it doesn’t execute immediately. Instead, it returns a **generator object** that can be iterated over.
2. When `next()` is called on the generator, the function executes until it encounters a `yield` statement, at which point it pauses and returns the yielded value.
3. The function can then be resumed from where it left off by calling `next()` again.

---

### **Simple Example of `yield`**

Let’s compare a normal function and a generator function.

#### Normal Function (Returns All at Once):
```python
def generate_numbers(n):
    result = []
    for i in range(n):
        result.append(i)
    return result

print(generate_numbers(5))
# Output: [0, 1, 2, 3, 4]
```

#### Generator Function (Using `yield`):
```python
def generate_numbers(n):
    for i in range(n):
        yield i

gen = generate_numbers(5)
print(next(gen))  # Output: 0
print(next(gen))  # Output: 1
print(next(gen))  # Output: 2
```

Here, the generator function doesn't create and return a full list. Instead, it produces the values one at a time as you iterate through it.

---

### **Key Benefits of `yield`**

1. **Memory Efficiency:**
   - A generator yields one item at a time, which is especially useful for large datasets. Instead of storing all items in memory, it computes and returns each item on demand.
   - Example:
     ```python
     def generate_large_numbers():
         for i in range(10**6):
             yield i

     gen = generate_large_numbers()
     print(next(gen))  # Only one number is in memory at a time
     ```

2. **Lazy Evaluation:**
   - Generators are **lazy**. They only compute the next value when explicitly asked (e.g., by `next()` or in a loop).

3. **Infinite Sequences:**
   - Since `yield` doesn’t require precomputing all values, it’s ideal for generating infinite or very large sequences.
   - Example:
     ```python
     def infinite_sequence():
         i = 0
         while True:
             yield i
             i += 1

     gen = infinite_sequence()
     print(next(gen))  # Output: 0
     print(next(gen))  # Output: 1
     ```

---

### **Using `yield` in Loops**

A common use of `yield` is in loops where you want to produce one value at a time.

**Example: Fibonacci Sequence Generator**
```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

fib = fibonacci()
for _ in range(5):
    print(next(fib))  # Output: 0, 1, 1, 2, 3
```

---

### **Difference Between `return` and `yield`**

| Feature                  | `return`                               | `yield`                                  |
|--------------------------|-----------------------------------------|------------------------------------------|
| **Function Execution**   | Terminates the function.               | Pauses the function and resumes later.   |
| **Value Produced**       | Returns a single value or object.      | Returns a generator that produces values one at a time. |
| **Memory Usage**         | Stores all values in memory.           | Generates values lazily (on demand).     |
| **Resumable?**           | No, function terminates after `return`. | Yes, resumes from where it paused.       |

---

### **Iterating Over a Generator**

A generator is iterable, which means you can use it in a `for` loop or convert it to a list.

#### Example 1: Iterating in a Loop
```python
def squares(n):
    for i in range(n):
        yield i * i

for square in squares(5):
    print(square)  # Output: 0, 1, 4, 9, 16
```

#### Example 2: Converting to a List
```python
def squares(n):
    for i in range(n):
        yield i * i

squares_list = list(squares(5))
print(squares_list)  # Output: [0, 1, 4, 9, 16]
```

---

### **Advanced Example: Combining Generators**

You can chain or compose generators for complex data pipelines.

**Example: Filtering and Transforming a Sequence**
```python
def numbers(n):
    for i in range(n):
        yield i

def even_numbers(generator):
    for number in generator:
        if number % 2 == 0:
            yield number

def double_numbers(generator):
    for number in generator:
        yield number * 2

gen = numbers(10)
even_gen = even_numbers(gen)
doubled_gen = double_numbers(even_gen)

for num in doubled_gen:
    print(num)  # Output: 0, 4, 8, 12, 16
```

---

### **When to Use `yield`**

1. **Large Data Sets:**
   - Use `yield` when you need to process large data sets or streams without loading everything into memory.

2. **Pipelines:**
   - Use `yield` to build pipelines where data flows through multiple stages of processing.

3. **Infinite Sequences:**
   - Use `yield` for generating infinite or dynamically generated sequences.

---

Here’s a list of **commonly used Python built-in variables**, along with brief examples:

### 1. **`__name__`**
- **Purpose**: Identifies whether a script is being run directly or imported as a module.
  
```python
# script.py
def my_function():
    print("Function in script")

if __name__ == "__main__":
    print("This script is being run directly")
else:
    print("This script is imported")
```

### 2. **`__file__`**
- **Purpose**: Contains the path to the current script or module.

```python
print(__file__)  # Outputs: /path/to/current/script.py
```

### 3. **`__doc__`**
- **Purpose**: Holds the documentation string of a module, class, or function.

```python
def example():
    """This function returns 'hello'."""
    return "hello"

print(example.__doc__)  # Outputs: This function returns 'hello'.
```

### 4. **`__dict__`**
- **Purpose**: Contains the attributes of a module, class, or instance in the form of a dictionary.

```python
class MyClass:
    def __init__(self, name):
        self.name = name

obj = MyClass("Python")
print(obj.__dict__)  # Outputs: {'name': 'Python'}
```

### 5. **`__annotations__`**
- **Purpose**: Contains type hints/annotations for functions or variables.

```python
def greet(name: str) -> str:
    return f"Hello, {name}"

print(greet.__annotations__)  # Outputs: {'name': <class 'str'>, 'return': <class 'str'>}
```

### 6. **`__version__`**
- **Purpose**: Used to indicate the version of a module or package (manually defined).

```python
__version__ = "1.0.0"
print(__version__)  # Outputs: 1.0.0
```

### 7. **`__class__`**
- **Purpose**: Refers to the class of an instance.

```python
class MyClass:
    pass

obj = MyClass()
print(obj.__class__)  # Outputs: <class '__main__.MyClass'>
```

### 8. **`__init__` and `__call__`**
- **Purpose**: `__init__` initializes a class, and `__call__` allows the instance to be used like a function.

```python
class MyClass:
    def __init__(self, value):
        self.value = value

    def __call__(self, new_value):
        self.value = new_value

obj = MyClass(10)
obj(20)
print(obj.value)  # Outputs: 20
```

### 9. **`__all__`**
- **Purpose**: Controls what gets imported with `from module import *`.

```python
__all__ = ['public_function']

def public_function():
    return "I am public"

def _private_function():
    return "I am private"
```

### 10. **`__repr__` and `__str__`**
- **Purpose**: `__repr__` provides an official string representation (for developers), while `__str__` provides a user-friendly string representation.

```python
class MyClass:
    def __repr__(self):
        return "MyClass()"

    def __str__(self):
        return "Instance of MyClass"

obj = MyClass()
print(repr(obj))  # Outputs: MyClass()
print(str(obj))   # Outputs: Instance of MyClass
```

### 11. **`__module__`**
- **Purpose**: Holds the name of the module in which a class or function is defined.

```python
class MyClass:
    pass

print(MyClass.__module__)  # Outputs: __main__ (if defined in the main script)
```

### 12. **`__builtins__`**
- **Purpose**: Contains a reference to the built-in module that holds Python’s built-in functions.

```python
print(__builtins__.print)  # Outputs: <built-in function print>
```

### 13. **`__import__`**
- **Purpose**: Allows dynamic importing of modules.

```python
math = __import__('math')
print(math.sqrt(16))  # Outputs: 4.0
```

### 14. **`__exit__` and `__enter__`**
- **Purpose**: Used in context managers (`with` statements) to define setup and teardown behavior.

```python
class MyContextManager:
    def __enter__(self):
        print("Entering the context")

    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting the context")

with MyContextManager():
    print("Inside the context")
```

### 15. **`__del__`**
- **Purpose**: Defines a destructor method for cleanup when an object is deleted.

```python
class MyClass:
    def __del__(self):
        print("Object is being deleted")

obj = MyClass()
del obj  # Outputs: Object is being deleted
```

### 16. **`__getitem__` and `__setitem__`**
- **Purpose**: Define custom behavior for accessing or assigning values to a class object using square brackets.

```python
class MyClass:
    def __init__(self):
        self.data = {}

    def __getitem__(self, key):
        return self.data.get(key)

    def __setitem__(self, key, value):
        self.data[key] = value

obj = MyClass()
obj['key'] = 'value'
print(obj['key'])  # Outputs: value
```

### 17. **`__iter__` and `__next__`**
- **Purpose**: Define iteration behavior for objects, making them iterable.

```python
class MyIterator:
    def __init__(self):
        self.n = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.n < 3:
            self.n += 1
            return self.n
        else:
            raise StopIteration

it = MyIterator()
for i in it:
    print(i)
```

### 18. **`__len__`**
- **Purpose**: Returns the length of an object (e.g., custom containers).

```python
class MyContainer:
    def __init__(self, items):
        self.items = items

    def __len__(self):
        return len(self.items)

container = MyContainer([1, 2, 3])
print(len(container))  # Outputs: 3
```

### 19. **`__call__`**
- **Purpose**: Allows instances of a class to be called like functions.

```python
class CallableClass:
    def __call__(self):
        print("Instance called like a function")

obj = CallableClass()
obj()  # Outputs: Instance called like a function
```

### 20. **`__hash__`**
- **Purpose**: Defines how the object is hashed (useful for using objects as dictionary keys).

```python
class MyClass:
    def __hash__(self):
        return 42

obj = MyClass()
print(hash(obj))  # Outputs: 42
```

Here's an overview of Python's core data structures—**list**, **tuple**, **dictionary (dict)**, **set**, and **string**—along with their properties, allowed operations, and typical use cases.

### 1. **List**
A list is an ordered, mutable (changeable) collection of items, which can include mixed data types.

| **Property**      | **Description**                                                                                         |
|-------------------|---------------------------------------------------------------------------------------------------------|
| Mutable           | Yes, items can be added, removed, or modified.                                                          |
| Ordered           | Yes, elements maintain insertion order.                                                                 |
| Indexed           | Yes, accessible via index (`list[i]`).                                                                  |
| Duplicate items   | Allowed, a list can contain multiple instances of the same item.                                        |

#### Operations
- **Create**: `my_list = [1, 2, 3]` or `my_list = list()`
- **Access**: `my_list[i]` (get item by index)
- **Modify**: `my_list[i] = new_value`
- **Add**: `my_list.append(value)`, `my_list.insert(index, value)`, `my_list.extend([val1, val2])`
- **Remove**: `my_list.remove(value)`, `my_list.pop(index)`, `del my_list[index]`
- **Concatenate**: `list1 + list2`
- **Slice**: `my_list[start:end:step]`

#### Usage
Lists are best when you need an ordered collection of items with the flexibility to modify, append, or remove elements. Commonly used for tasks where item order and mutability are important, like maintaining a stack, queue, or dynamic collection.

---

### 2. **Tuple**
A tuple is an ordered, immutable collection of items, often used to store heterogeneous data.

| **Property**      | **Description**                                                                                         |
|-------------------|---------------------------------------------------------------------------------------------------------|
| Mutable           | No, tuples are immutable once created.                                                                  |
| Ordered           | Yes, elements maintain insertion order.                                                                 |
| Indexed           | Yes, accessible via index (`tuple[i]`).                                                                 |
| Duplicate items   | Allowed, can contain multiple instances of the same item.                                               |

#### Operations
- **Create**: `my_tuple = (1, 2, 3)` or `my_tuple = tuple([1, 2, 3])`
- **Access**: `my_tuple[i]`
- **Concatenate**: `tuple1 + tuple2`
- **Slice**: `my_tuple[start:end:step]`
- **Unpack**: `a, b, c = my_tuple`

#### Usage
Tuples are suitable for fixed collections of items, like a record or coordinates, and often used for "read-only" data where immutability is preferred for performance and safety.

---

### 3. **Dictionary (dict)**
A dictionary is an unordered collection of key-value pairs, where each key is unique and maps to a specific value.

| **Property**      | **Description**                                                                                         |
|-------------------|---------------------------------------------------------------------------------------------------------|
| Mutable           | Yes, you can add, remove, or modify key-value pairs.                                                    |
| Ordered           | Yes, since Python 3.7, dictionaries maintain insertion order.                                           |
| Indexed           | No, accessed by unique keys.                                                                            |
| Duplicate keys    | Not allowed, each key must be unique.                                                                   |

#### Operations
- **Create**: `my_dict = {"key1": "value1", "key2": "value2"}` or `my_dict = dict()`
- **Access**: `my_dict["key"]`
- **Add/Update**: `my_dict["new_key"] = "new_value"`
- **Remove**: `my_dict.pop("key")`, `del my_dict["key"]`, `my_dict.clear()`
- **Check existence**: `'key' in my_dict`
- **Get keys/values**: `my_dict.keys()`, `my_dict.values()`, `my_dict.items()`

#### Usage
Dictionaries are ideal when you need to store pairs of unique keys and values, such as lookup tables or when performing fast searches by key.

---

### 4. **Set**
A set is an unordered, mutable collection of unique items, useful for removing duplicates and performing mathematical operations.

| **Property**      | **Description**                                                                                         |
|-------------------|---------------------------------------------------------------------------------------------------------|
| Mutable           | Yes, can add or remove elements, but individual elements cannot be modified.                            |
| Ordered           | No, does not maintain order.                                                                            |
| Indexed           | No, elements cannot be accessed by index.                                                               |
| Duplicate items   | Not allowed, only unique elements are stored.                                                           |

#### Operations
- **Create**: `my_set = {1, 2, 3}` or `my_set = set([1, 2, 3])`
- **Add**: `my_set.add(value)`
- **Remove**: `my_set.remove(value)`, `my_set.discard(value)`, `my_set.pop()`
- **Union**: `set1 | set2` or `set1.union(set2)`
- **Intersection**: `set1 & set2` or `set1.intersection(set2)`
- **Difference**: `set1 - set2` or `set1.difference(set2)`

#### Usage
Sets are well-suited for operations involving unique items or mathematical set operations, such as eliminating duplicates or finding common elements across collections.

---

### 5. **String**
A string is an ordered, immutable sequence of characters used to store and manipulate text.

| **Property**      | **Description**                                                                                         |
|-------------------|---------------------------------------------------------------------------------------------------------|
| Mutable           | No, strings are immutable once created.                                                                 |
| Ordered           | Yes, characters maintain insertion order.                                                               |
| Indexed           | Yes, accessible via index (`string[i]`).                                                                |
| Duplicate items   | Allowed, can contain repeated characters.                                                               |

#### Operations
- **Create**: `my_string = "hello"`
- **Access**: `my_string[i]`
- **Concatenate**: `"hello" + " world"`
- **Slice**: `my_string[start:end:step]`
- **Search**: `"substring" in my_string`
- **Methods**: `my_string.upper()`, `my_string.lower()`, `my_string.strip()`, `my_string.split(delimiter)`

#### Usage
Strings are essential for handling textual data, used in everything from user input to data processing. Strings are often used with text processing methods like searching, splitting, and transforming data into different formats.

---

### Summary Table of Properties

| Data Structure | Mutable | Ordered | Indexed | Duplicates | Access Method       |
|----------------|---------|---------|---------|------------|---------------------|
| List           | Yes     | Yes     | Yes     | Allowed    | `list[i]`           |
| Tuple          | No      | Yes     | Yes     | Allowed    | `tuple[i]`          |
| Dictionary     | Yes     | Yes*    | No      | No (keys)  | `dict[key]`         |
| Set            | Yes     | No      | No      | Not allowed| -                   |
| String         | No      | Yes     | Yes     | Allowed    | `string[i]`         |

> \* Dictionaries are ordered as of Python 3.7


# Python Coding Conventions

## 1. File Naming
- Use lowercase letters with underscores as word separators.
- **Good:** `my_file.py`
- **Bad:** `MyFile.py`, `my-file.py`

## 2. Line Length
- Limit lines to 79 characters.
- For long strings, use parentheses to break them up.

## 3. Indentation
- Use 4 spaces per indentation level.
- Do not use tabs.

## 4. Blank Lines
- Use blank lines to separate functions and classes.
- Surround top-level function and class definitions with two blank lines.
- Method definitions within a class are surrounded by a single blank line.

## 5. Imports
- Imports should usually be on separate lines.
- Order imports as follows:
  - Standard library imports
  - Related third-party imports
  - Local application/library-specific imports
- Leave a blank line between each group of imports.

## 6. Whitespace in Expressions and Statements
- Avoid extra spaces in expressions and statements.
- **Good:** `if condition:`
- **Bad:** `if condition :`

## 7. Comments
- Use comments to explain why code does something, not what it does.
- Use inline comments sparingly and only when necessary.
- Write comments in English.

## 8. Naming Conventions
- **Variables:** Use lowercase letters with underscores (e.g., `my_variable`).
- **Constants:** Use uppercase letters with underscores (e.g., `MY_CONSTANT`).
- **Classes:** Use CapitalizedWords convention (e.g., `MyClass`).
- **Functions:** Use lowercase letters with underscores (e.g., `my_function`).

## 9. Docstrings
- Use triple quotes for docstrings to describe modules, classes, and functions.
- Docstrings should be placed immediately after the definition line.

## 10. Exceptions
- Use exceptions to handle errors, and avoid using return codes.
- Use specific exceptions (e.g., `ValueError`) instead of a generic exception.

## 11. Function Definitions
- Function names should be descriptive and use lowercase with underscores.
- Use default parameter values where appropriate.
- Avoid ambiguous abbreviations.

## 12. Type Hints
- Use type hints to specify expected argument types and return types for functions.

## Example Python Code Following Conventions

```python
# Importing standard library
import os
import sys

# Importing third-party library
import requests

# Importing local application/library-specific imports
from my_module import MyClass

class MyClass:
    """A simple example class."""
    
    def __init__(self, value: int):
        """Initialize with a value."""
        self.value = value

    def get_value(self) -> int:
        """Return the stored value."""
        return self.value

def my_function(param1: str, param2: int) -> None:
    """Process the input parameters."""
    if param2 > 0:
        print(f"Processing {param1} with value {param2}")
    
    # Return early if condition is met
    return

# Example usage
if __name__ == "__main__":
    my_function("example", 5)
```
- subset-order doesnt matter

- subsequence-maintain order of sequence

- subarray,substring- contigous chunk

