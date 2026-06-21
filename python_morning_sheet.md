# PYTHON EXAM — MORNING SHEET
## Topics split: THEORY (explain in words) vs CODE (write working code)
## Read once. Write once. Move on. 10 min per topic.

---

## 1. CONDITIONAL STATEMENTS + OUTPUT PREDICTION
### [CODE DOMINATED]

**Say out loud:** "if elif else, truthy falsy, watch the tricky outputs"

**Core syntax:**
```python
# Basic if-elif-else structure
x = 10
if x > 15:
    print("big")
elif x > 5:          # elif checked only if first condition False
    print("medium")
else:
    print("small")    # runs only if ALL above are False
```

**Tricky output pattern (common exam trap):**
```python
# 0 is treated as False, non-zero as True
if 0:
    print("Zero is True")
else:
    print("Zero is False")     # THIS prints — 0 is falsy

# 'or' returns first truthy value it finds, 'and' returns first falsy
if False or True and False:
    print("Condition met")
else:
    print("Condition not met")  # check 'and' before 'or' (precedence!)
# Step: True and False = False
# Step: False or False = False -> else runs
```

**Key rule to remember:** `and` has higher precedence than `or`. Always evaluate `and` first when reading mixed conditions.

**Falsy values in Python (memorize this list):** `0`, `0.0`, `""`, `[]`, `{}`, `()`, `None`, `False`

---

## 2. STRING OPERATIONS
### [CODE DOMINATED]

**Say out loud:** "slice with start:stop:step, len for last char, vowels removed"

**Slicing syntax:**
```python
s = "PYTHON PROGRAMMING"

print(s[2:15:2])    # start=2, stop=15, step=2 -> every 2nd char
print(s[-3:-16:-2]) # negative indices count from end, negative step goes backward
print(s[:13])        # from start to index 13
print(s[6:])         # from index 6 to end
print(s[:-2])        # everything except last 2 chars
print(s[3:14:3])     # start=3, stop=14, step=3
```

**Access last character using len():**
```python
def last_char(s):
    # len(s) gives total length, subtract 1 for zero-based index
    return s[len(s) - 1]

print(last_char("hello"))   # prints 'o'
```

**Remove vowels from string:**
```python
def remove_vowels(s):
    vowels = "aeiouAEIOU"
    result = ""
    for ch in s:               # loop through every character
        if ch not in vowels:   # keep only non-vowel characters
            result += ch
    return result

text = input("Enter a string: ")
print(remove_vowels(text))
```

**Palindrome check:**
```python
def is_palindrome(s):
    s = s.lower()           # normalize case
    return s == s[::-1]     # compare string with its reverse

word = input("Enter a string: ")
if is_palindrome(word):
    print("Palindrome")
else:
    print("Not a Palindrome")
```

---

## 3. FUNCTIONS — ARGUMENT TYPES
### [THEORY + CODE]

**Say out loud:** "positional, keyword, default, *args, **kwargs"

**Theory:**

Python supports four main types of function arguments:

- **Positional arguments:** passed in order, matched by position
- **Keyword arguments:** passed as name=value, order doesn't matter
- **Default arguments:** have a pre-set value if caller doesn't provide one
- **Variable-length arguments:** `*args` collects extra positional args into a tuple, `**kwargs` collects extra keyword args into a dictionary

**Formal vs Actual arguments:**
- **Formal parameters** = the variable names listed in the function definition
- **Actual arguments** = the real values passed when calling the function

```python
def greet(name, age):   # 'name' and 'age' are FORMAL parameters
    print(f"{name} is {age} years old")

greet("Riya", 20)        # "Riya" and 20 are ACTUAL arguments
```

**Code — all 4 types together:**
```python
def demo(a, b=10, *args, **kwargs):
    # a -> positional, required
    # b -> default, used if not provided
    # args -> tuple of extra positional arguments
    # kwargs -> dict of extra keyword arguments
    print("a:", a)
    print("b:", b)
    print("args:", args)
    print("kwargs:", kwargs)

demo(1, 2, 3, 4, x=5, y=6)
# Output:
# a: 1
# b: 2
# args: (3, 4)
# kwargs: {'x': 5, 'y': 6}
```

**Multiple return values:**
```python
def min_max(numbers):
    return min(numbers), max(numbers)   # returns a tuple automatically

low, high = min_max([4, 1, 9, 2])   # unpacked into two variables
print(low, high)   # 1 9
```

---

## 4. LAMBDA + MAP/FILTER
### [CODE DOMINATED]

**Say out loud:** "lambda is anonymous function, map transforms, filter selects"

**Lambda syntax:**
```python
# lambda arguments: expression  (no 'return' needed, single expression only)
square = lambda x: x * x
print(square(5))     # 25
```

**Lambda to return even numbers from a list:**
```python
nums = [1, 2, 3, 4, 5, 6, 7, 8]
evens = list(filter(lambda x: x % 2 == 0, nums))
# filter() keeps elements where lambda returns True
print(evens)   # [2, 4, 6, 8]
```

**map() — transform every element:**
```python
nums = [1, 2, 3, 4]
squared = list(map(lambda x: x * x, nums))
print(squared)   # [1, 4, 9, 16]
```

---

## 5. RECURSION
### [CODE DOMINATED]

**Say out loud:** "function calls itself, must have base case to stop"

```python
def factorial(n):
    if n == 0 or n == 1:    # BASE CASE - stops recursion
        return 1
    return n * factorial(n - 1)   # RECURSIVE CASE - calls itself with smaller input

print(factorial(5))   # 5*4*3*2*1 = 120
```

**Key rule:** Every recursive function needs a base case, or it recurses forever (stack overflow).

---

## 6. LIST METHODS + SORTING
### [CODE DOMINATED]

**Say out loud:** "pop removes by index, remove removes by value, append adds end, insert adds at position"

**Method comparison:**
```python
lst = [10, 20, 30, 40]

lst.pop(1)        # removes element AT INDEX 1 -> removes 20, returns it
lst.remove(30)    # removes the FIRST OCCURRENCE OF VALUE 30

lst2 = [1, 2, 3]
lst2.append(4)        # adds 4 at the END only
lst2.insert(1, 99)    # adds 99 AT INDEX 1 (shifts others right)
```

**Difference table:**
| Method | Removes/Adds by | Use when |
|--------|------------------|----------|
| pop(i) | index | you know position |
| remove(x) | value | you know the value |
| append(x) | always at end | adding to end |
| insert(i,x) | at specific index | inserting in middle |

**Selection sort (must write from scratch):**
```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):     # find smallest in remaining unsorted part
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]   # swap smallest into position i
    return arr

print(selection_sort([5, 2, 9, 1, 5]))   # [1, 2, 5, 5, 9]
```

**Nested list traversal pattern (matrix multiplication):**
```python
def multiply_matrices(A, B):
    rows_A, cols_A = len(A), len(A[0])
    rows_B, cols_B = len(B), len(B[0])
    
    # result matrix filled with zeros
    result = [[0 for _ in range(cols_B)] for _ in range(rows_A)]
    
    for i in range(rows_A):
        for j in range(cols_B):
            for k in range(cols_A):           # shared dimension
                result[i][j] += A[i][k] * B[k][j]
    return result

A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]
print(multiply_matrices(A, B))   # [[19, 22], [43, 50]]
```

---

## 7. DICTIONARY OPERATIONS
### [CODE DOMINATED]

**Say out loud:** "key value pairs, sorted printing, search and insert if missing"

```python
friends = {"Aman": "9876543210", "Riya": "8765432109", "Karan": "7654321098"}

# print dictionary sorted by key (name)
for name in sorted(friends):
    print(name, ":", friends[name])

# search for a name, add if missing
search_name = input("Enter name to search: ")
if search_name in friends:
    print("Found:", friends[search_name])
else:
    new_number = input("Not found. Enter phone number to add: ")
    friends[search_name] = new_number    # adds new key-value pair
    print("Added successfully")
```

**Dictionary creation methods (theory bit):**
```python
d1 = {"a": 1, "b": 2}              # literal
d2 = dict(a=1, b=2)                # using dict() constructor
d3 = dict([("a", 1), ("b", 2)])    # from list of tuples
d4 = {}.fromkeys(["a", "b"], 0)    # fromkeys - same default value for all keys
```

---

## 8. CLASSES, OBJECTS, __init__
### [THEORY + CODE]

**Say out loud:** "class is blueprint, object is instance, init runs automatically on creation"

**Theory:**

A **class** is a blueprint/template defining attributes and behaviors. An **object** is a specific instance created from that class. The `__init__` method is a constructor — it runs automatically whenever a new object is created, used to initialize the object's attributes.

**Why __init__ is needed:** Without it, every object would start with no attributes set, requiring manual assignment after creation every single time. __init__ ensures every object is properly initialized in one step at creation.

```python
class Student:
    def __init__(self, name, marks):
        # self refers to the specific object being created
        self.name = name
        self.marks = marks
    
    def display(self):
        print(f"{self.name} scored {self.marks}")

s1 = Student("Aman", 85)   # __init__ runs automatically here
s1.display()                # Aman scored 85
```

**Passing object as argument to a function:**
```python
def show_details(student_obj):    # accepts an object as parameter
    print(f"Name: {student_obj.name}, Marks: {student_obj.marks}")

s1 = Student("Riya", 92)
show_details(s1)    # passing the object itself
```

---

## 9. CLASSMETHOD vs STATICMETHOD
### [THEORY]

**Say out loud:** "classmethod gets cls, modifies class data. staticmethod gets nothing, just utility"

**Theory only — write this paragraph:**

A `@classmethod` takes `cls` (the class itself) as its first parameter instead of `self`. It can access and modify class-level variables shared across all instances. It is typically used for alternative constructors or operations affecting the whole class.

A `@staticmethod` takes neither `self` nor `cls`. It behaves like a regular function that happens to live inside a class for organizational purposes — it cannot access or modify instance or class data directly.

**Key difference:** classmethod is class-aware, staticmethod is completely independent of class/instance state.

```python
class MathHelper:
    count = 0   # class variable

    @classmethod
    def increment_count(cls):
        cls.count += 1     # modifies class-level data

    @staticmethod
    def add(a, b):
        return a + b        # pure utility, no class/instance access needed

MathHelper.increment_count()
print(MathHelper.add(3, 4))   # 7
```

---

## 10. INHERITANCE + super()
### [THEORY + CODE]

**Say out loud:** "child inherits parent, super calls parent method"

**Theory:**

Inheritance allows a class (child/derived class) to acquire attributes and methods from another class (parent/base class), promoting code reuse. The child class can use parent functionality directly, override it with its own version, or extend it.

`super()` is used inside the child class to call the parent class's methods, commonly used inside `__init__` to ensure the parent's initialization logic still runs before adding child-specific setup.

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        print(f"{self.name} makes a sound")

class Dog(Animal):                  # Dog inherits from Animal
    def __init__(self, name, breed):
        super().__init__(name)      # calls Animal's __init__ first
        self.breed = breed
    
    def speak(self):                 # method overriding
        print(f"{self.name} barks")

d = Dog("Rex", "Labrador")
d.speak()    # Rex barks (overridden version runs)
```

---

## 11. EXCEPTION HANDLING
### [THEORY + CODE]

**Say out loud:** "try block risky code, except catches error, finally always runs"

**Theory:**

Exception handling allows a program to gracefully respond to runtime errors instead of crashing. The `try` block contains code that might raise an error. The `except` block catches and handles a specific (or general) exception type. The `else` block runs only if no exception occurred. The `finally` block always runs, regardless of whether an exception occurred — typically used for cleanup (closing files, releasing resources).

```python
try:
    num = int(input("Enter a number: "))
    result = 10 / num
except ZeroDivisionError:
    print("Cannot divide by zero")
except ValueError:
    print("Invalid input, must be a number")
else:
    print("Result:", result)     # runs only if no exception
finally:
    print("Execution complete")   # ALWAYS runs
```

---

## 12. FILE HANDLING + CSV
### [CODE DOMINATED]

**Say out loud:** "open read write append, csv reader and writer"

**File opening modes:**
| Mode | Meaning |
|------|---------|
| 'r' | read (file must exist) |
| 'w' | write (overwrites/creates) |
| 'a' | append (adds to end) |
| 'r+' | read and write |
| 'rb'/'wb' | binary mode |

**Basic file read/write:**
```python
# Writing to a file
with open("data.txt", "w") as f:    # 'with' auto-closes the file
    f.write("Hello World")

# Reading from a file
with open("data.txt", "r") as f:
    content = f.read()
    print(content)
```

**File methods:**
```python
with open("data.txt", "r") as f:
    f.read(5)        # reads first 5 characters
    f.seek(0)        # moves cursor back to start
    print(f.tell())  # returns current cursor position
```

**CSV reading:**
```python
import csv

with open("data.csv", "r") as f:
    reader = csv.reader(f)
    for row in reader:        # each row is a list of strings
        print(row)
```

**CSV writing:**
```python
import csv

with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["Name", "Age"])     # write header
    writer.writerow(["Aman", 20])         # write data row
```

---

## 13. UNIT TESTING (unittest / doctest / pytest)
### [THEORY + CODE]

**Say out loud:** "unittest classes with assert methods, doctest inside docstrings, pytest just uses plain assert"

**Theory:**

**unittest** is Python's built-in testing framework. Test cases are written as methods inside a class that inherits from `unittest.TestCase`. Assertion methods like `assertEqual`, `assertTrue`, `assertRaises` are used to verify expected behavior.

**doctest** allows writing tests directly inside a function's docstring, formatted to look like an interactive Python session. Running `doctest.testmod()` automatically executes these embedded tests.

**pytest** is a simpler, more modern testing framework. Tests are plain functions starting with `test_`, using Python's built-in `assert` statement directly, without needing a class structure.

```python
# unittest example
import unittest

def add(a, b):
    return a + b

class TestAdd(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)    # checks if add(2,3) equals 5

if __name__ == "__main__":
    unittest.main()
```

```python
# doctest example
def add(a, b):
    """
    >>> add(2, 3)
    5
    """
    return a + b

import doctest
doctest.testmod()    # runs the test written inside the docstring
```

```python
# pytest example (saved as test_file.py, run with: pytest test_file.py)
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5    # plain assert, no class needed
```

---

## 14. NUMPY BASICS
### [CODE DOMINATED]

**Say out loud:** "array creation, reshape, slicing, aggregate operations"

```python
import numpy as np

# Array creation
a = np.array([1, 2, 3, 4, 5, 6])
zeros = np.zeros((2, 3))      # 2x3 array of zeros
ones = np.ones((3, 3))         # 3x3 array of ones
ranged = np.arange(0, 10, 2)   # like range() but returns array: [0,2,4,6,8]

# Reshape - change array dimensions (must have same total elements)
b = a.reshape(2, 3)    # converts 1D array of 6 elements into 2 rows x 3 cols

# Slicing
print(a[1:4])       # elements index 1 to 3
print(b[:, 1])       # all rows, column index 1 only

# ndim - number of dimensions
print(b.ndim)    # 2 (since it's a 2D array)

# Aggregate operations
print(a.sum())     # sum of all elements
print(a.mean())    # average
print(a.max())      # maximum value
```

**NumPy array vs nested Python list — advantages:**
- Faster execution (implemented in C internally)
- Element-wise operations work directly (a + b adds element-wise, lists would concatenate)
- Less memory usage
- Built-in mathematical/statistical functions

---

## 15. TYPE ANNOTATIONS + PEP 8
### [THEORY]

**Say out loud:** "type hints document expected types, PEP8 is style guide"

**Theory only:**

Type annotations (PEP 484) let you specify the expected data type of variables, function parameters, and return values, without Python enforcing them at runtime — they're primarily for documentation and tools like `mypy` to catch type errors before running the code.

```python
def add(a: int, b: int) -> int:    # a and b expected int, return type int
    return a + b

name: str = "Aman"     # variable type hint
```

PEP 8 is Python's official style guide — covering naming conventions (snake_case for functions/variables, PascalCase for classes), indentation (4 spaces), line length limits, and code organization, ensuring consistent, readable code across different developers.

---

# IF SHORT ON TIME — DO ONLY THESE 8

1. Conditional + output prediction
2. String operations (slicing, palindrome, vowels)
3. Functions — argument types + formal/actual
4. List methods + selection sort
5. Dictionary operations
6. Classes + __init__ + passing objects
7. Inheritance + super()
8. Exception handling

These 8 cover Q1 shorts + at least one full question from every likely unit choice.

---

# YOUR TIMER PLAN

15 topics x 10 min = 150 min (2.5 hours) for full pass.
8 topics x 10 min = 80 min for the cut-down version.

Read -> Type/write the code once by hand -> move on. Don't just read code, actually type it out — muscle memory matters more for Python than for theory subjects.
