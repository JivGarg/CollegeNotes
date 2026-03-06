# PYTHON PROGRAMMING — UNIT 1 DETAILED NOTES

> **Source:** PPT (cfb12c9e-d062-431e-b188-e67686b8bab2.pdf), supplementary PDFs (Comprehensions, List Ops, Dict Ops), Python official docs, PEP 634, and reference links.

---

## 1. Identifiers

An **identifier** is the name given to a variable, function, class, object, module, or any other user-defined item in Python.

- **Rules for Naming**
  - Can contain letters (`A-Z`, `a-z`), digits (`0-9`), and underscores (`_`)
  - **Cannot** start with a digit (e.g., `1student` is invalid)
  - **Cannot** contain special characters like `@`, `%`, `#`, `-`
  - **Cannot** be a Python keyword (`if`, `else`, `for`, `while`, `class`, etc.)
  - Python identifiers are **case-sensitive** — `Age` and `age` are different identifiers

- **Valid vs Invalid Examples**

  | Valid         | Invalid          | Reason                |
  |---------------|------------------|-----------------------|
  | `Name`        | `1student`       | Starts with a digit   |
  | `Max_marks`   | `total-marks`    | Contains hyphen       |
  | `_average`    | `class`          | Reserved keyword      |
  | `subject1`    | `@value`         | Special character     |

- **Types of Identifiers**
  - **Variable Identifiers** — store data
    ```python
    age = 14
    price = 20.50
    ```
  - **Function Identifiers** — define functions
    ```python
    def calculate_sum(a, b):
        return a + b
    ```
  - **Class Identifiers** — define classes
    ```python
    class Student:
        pass
    ```

- **Note:** Python follows the Unicode standard for identifiers (PEP 3131), so non-ASCII letters like `résumé` or `переменная` are technically valid, though not recommended for general use.

---

## 2. Keywords

**Keywords** are reserved words with special meaning that **cannot** be used as identifiers.

- **Properties**
  - Case-sensitive (mostly lowercase)
  - Cannot be used as variable, function, or class names
  - Fixed meaning defined by the language

- **Categories of Python Keywords**

  | Category                 | Keywords                                          |
  |--------------------------|---------------------------------------------------|
  | Control Flow             | `if`, `else`, `elif`, `for`, `while`, `break`, `continue`, `pass` |
  | Function & Class         | `def`, `return`, `lambda`, `class`                |
  | Logical                  | `and`, `or`, `not`                                |
  | Exception Handling       | `try`, `except`, `finally`, `raise`               |
  | Variable & Value         | `True`, `False`, `None`                           |
  | Import                   | `import`, `from`, `as`                            |
  | Scope                    | `global`, `nonlocal`                              |
  | Context                  | `with`                                            |
  | Iterator/Generator       | `yield`, `in`                                     |
  | Identity/Deletion        | `is`, `del`                                       |
  | Pattern Matching (3.10+) | `match`, `case` (soft keywords)                   |

- **Keywords vs Identifiers**

  | Keywords           | Identifiers           |
  |--------------------|-----------------------|
  | Reserved words     | User-defined names    |
  | Fixed meaning      | Meaning defined by user |
  | Cannot be renamed  | Can be renamed        |
  | e.g. `if`          | e.g. `count`          |

- **Soft Keywords** (`match`, `case`): These are context-sensitive — they act as keywords only inside a `match` statement and can be used as variable names elsewhere.

---

## 3. Indentation

Python uses **indentation** (whitespace at the beginning of a line) to define blocks of code, instead of braces `{}` like C/Java.

- **Key Points**
  - Indentation indicates a **block of code** (body of `if`, `for`, `def`, `class`, etc.)
  - All statements at the **same indentation level** belong to the **same block**
  - Standard practice: **4 spaces** per indentation level (PEP 8)
  - Mixing **tabs and spaces** is **not allowed** in Python 3 (raises `TabError`)

- **Correct Example**
  ```python
  if 5 > 2:
      print("Five is greater than two!")
      print("This is inside the if block")
  ```

- **Incorrect Examples**
  ```python
  # ERROR: missing indentation
  if 5 > 2:
  print("Five is greater than two!")   # IndentationError

  # ERROR: inconsistent indentation
  if 5 > 2:
      print("Five is greater than two!")
          print("This line has extra indent")  # IndentationError: unexpected indent
  ```

- **Why indentation matters:** It's not just cosmetic — it's **syntactically required**. Incorrect indentation changes program logic or causes errors.

---

## 4. Comments

**Comments** are lines that the Python interpreter ignores. They explain code, improve readability, and can disable code during testing.

- **Single-line Comments**
  - Start with `#`
  - Everything after `#` on that line is ignored
  ```python
  # This is a comment
  print("Hello, World!")

  print("Hello, World!")  # This is an inline comment
  ```

- **Multi-line Comments**
  - Python has no dedicated multi-line comment syntax
  - Use multiple `#` lines, or use a multi-line string (triple quotes) as a workaround (though technically it's a string literal, not a comment)
  ```python
  # This is line 1 of a comment
  # This is line 2 of a comment

  """
  This is sometimes used as a
  multi-line comment (but it's actually a string literal).
  """
  ```

- **Best Practice (PEP 8):** Put comments on their own line when possible. Keep comments concise and relevant.

---

## 5. Documentation Strings (Docstrings)

**Docstrings** are special string literals used to describe what a module, function, class, or method does.

- **Syntax**
  - Written using **triple quotes**: `""" """` (recommended) or `''' '''`
  - Placed **immediately after** the definition of a module, function, class, or method
  - Stored in memory as the `__doc__` attribute

- **Types of Docstrings**
  - **Module Docstring** — describes the entire file
    ```python
    """
    This module performs basic arithmetic operations.
    """
    ```
  - **Function Docstring** — explains what a function does
    ```python
    def calculate_sum(a, b):
        """Returns the sum of two numbers."""
        return a + b
    ```
  - **Class Docstring** — explains a class
    ```python
    class Student:
        """Represents a student with name and marks."""
        pass
    ```
  - **Method Docstring** — explains a method inside a class
    ```python
    class Student:
        def display(self):
            """Displays student details."""
            print("Student info")
    ```

- **Accessing Docstrings**
  ```python
  print(calculate_sum.__doc__)   # Output: Returns the sum of two numbers.
  help(calculate_sum)            # Shows formatted docstring
  ```

- **Conventions (PEP 257)**
  - First line: short, concise summary ending with a period
  - Second line: blank (separates summary from description)
  - Following lines: describe calling conventions, side effects, etc.

---

## 6. Unicode and Encoding

- **Unicode**
  - A universal character standard that assigns a unique number (**code point**) to every character in virtually all writing systems
  - Examples:

    | Character | Unicode Code Point |
    |-----------|--------------------|
    | A         | U+0041             |
    | a         | U+0061             |
    | ₹         | U+20B9             |
    | 😊        | U+1F60A            |
    | क         | U+0915             |

- **Python 3 Strings and Unicode**
  - In Python 3, **all `str` objects are Unicode** by default
  - No separate `unicode` type (unlike Python 2)
  ```python
  text = "Hello"
  type(text)        # <class 'str'>  (Unicode string)
  ```

- **Encoding (str → bytes)**
  - Converting a Unicode string into a byte representation using a specific encoding (e.g., UTF-8)
  ```python
  text = "Hello"
  encoded_text = text.encode("utf-8")
  # encoded_text → b'Hello'
  # type(encoded_text) → <class 'bytes'>
  ```

- **Decoding (bytes → str)**
  ```python
  decoded_text = encoded_text.decode("utf-8")
  # decoded_text → "Hello"
  ```

- **Common Encodings**
  - **UTF-8** — variable-length (1–4 bytes), most common on the web, backward-compatible with ASCII
  - **UTF-16** — used internally by some systems (e.g., Windows)
  - **ASCII** — 7-bit, only covers English characters (0–127)
  - **Latin-1 (ISO 8859-1)** — 8-bit, covers Western European languages

- **Python Source Encoding**
  - Default source file encoding in Python 3 is **UTF-8**
  - Can be changed with a magic comment at the top of a file: `# -*- coding: utf-8 -*-`

---

## 7. Data Types and Type Hints

### 7.1 Data Types

Python has the following built-in data types:

| Category    | Data Type    | Example              | Mutable? | Ordered? | Duplicates? |
|-------------|-------------|----------------------|----------|----------|-------------|
| Numeric     | `int`       | `42`, `-7`           | No       | N/A      | N/A         |
| Numeric     | `float`     | `3.14`, `-0.01`      | No       | N/A      | N/A         |
| Numeric     | `complex`   | `2 + 3j`             | No       | N/A      | N/A         |
| Text        | `str`       | `"Hello"`            | No       | Yes      | Yes         |
| Sequence    | `list`      | `[1, "apple", 3]`   | Yes      | Yes      | Yes         |
| Sequence    | `tuple`     | `(1, "apple", 3)`   | No       | Yes      | Yes         |
| Sequence    | `range`     | `range(0, 10)`       | No       | Yes      | Yes         |
| Mapping     | `dict`      | `{"age": 30}`        | Yes      | Yes*     | Keys: No    |
| Set         | `set`       | `{1, 2, 3}`          | Yes      | No       | No          |
| Set         | `frozenset` | `frozenset({1, 2})`  | No       | No       | No          |
| Boolean     | `bool`      | `True`, `False`      | No       | N/A      | N/A         |
| Binary      | `bytes`     | `b"hello"`           | No       | Yes      | Yes         |
| Binary      | `bytearray` | `bytearray(5)`      | Yes      | Yes      | Yes         |
| Null        | `NoneType`  | `None`               | No       | N/A      | N/A         |

> \*`dict` is insertion-ordered since Python 3.7+

- **Dynamic Typing:** Python automatically determines the data type at runtime
  ```python
  age = 20          # int
  price = 99.5      # float
  name = "Ritika"   # str
  is_pass = True    # bool
  ```

- **Getting the Data Type:**
  ```python
  type(age)         # <class 'int'>
  type(name)        # <class 'str'>
  ```

### 7.2 Type Hints

**Type hints** (PEP 484) indicate the expected data types for variables and function arguments. They do **not enforce** types at runtime — they are for documentation, readability, and static analysis tools (e.g., `mypy`, Pylance).

- **Variable Type Hints**
  ```python
  age: int = 20
  price: float = 99.5
  name: str = "Ritika"
  is_pass: bool = True
  ```

- **Function Type Hints**
  ```python
  def add(a: int, b: int) -> int:
      return a + b
  # a and b should be integers; function returns an integer
  ```

- **Type Hints with Collections**
  ```python
  marks: list[int] = [90, 85, 88]
  student: dict[str, int] = {
      "math": 90,
      "science": 85
  }
  # student → dict where keys are str, values are int
  ```

- **Optional and Union (from `typing` module)**
  ```python
  from typing import Optional, Union
  value: Optional[int] = None          # int or None
  data: Union[int, str] = "hello"      # int or str
  ```

- **Python 3.10+ shorthand:**
  ```python
  data: int | str = "hello"
  ```

---

## 8. Object Identity vs Equality

### 8.1 Identity (`is` operator)
- Checks whether two variables **refer to the same object in memory** (same `id()`)
- Even if two objects have identical values, `is` returns `False` if they are **different objects**

```python
x = [1, 2, 3]
y = [1, 2, 3]
z = x

print(x is y)   # False — different objects in memory
print(x is z)   # True  — z points to the same object as x
print(id(x), id(y), id(z))
```

### 8.2 Equality (`==` operator)
- Checks whether two objects have the **same value/content**
- Does **not** care about memory location

```python
x = [1, 2, 3]
y = [1, 2, 3]

print(x == y)   # True  — same content
print(x is y)   # False — different objects
```

### 8.3 Summary Table

| Aspect       | `is` (Identity)                  | `==` (Equality)           |
|-------------|----------------------------------|---------------------------|
| Compares    | Memory address (`id()`)          | Value / Content           |
| Returns     | `True` if same object            | `True` if same value      |
| Use case    | Checking singletons (`None`)     | Comparing values          |

- **Best Practice:** Use `is` only for singletons like `None`:
  ```python
  if x is None:
      ...
  ```

- **CPython Optimization Note:** Small integers (`-5` to `256`) and short strings are often **interned** (cached), so `is` may return `True` for them — but **do not rely on this**.

---

## 9. Operator Precedence and Associativity

### 9.1 Types of Operators

1. **Arithmetic Operators:** `+`, `-`, `*`, `/`, `%`, `**`, `//`
2. **Assignment Operators:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `//=`, `**=`, `&=`, `|=`, `^=`, `>>=`, `<<=`, `:=`
3. **Comparison Operators:** `==`, `!=`, `>`, `<`, `>=`, `<=`
4. **Logical Operators:** `and`, `or`, `not`
5. **Identity Operators:** `is`, `is not`
6. **Membership Operators:** `in`, `not in`
7. **Bitwise Operators:** `&`, `|`, `^`, `~`, `<<`, `>>`

### 9.2 Arithmetic Operators Detail

| Operator | Name              | Example  | Notes                                 |
|----------|-------------------|----------|---------------------------------------|
| `+`      | Addition          | `x + y`  |                                       |
| `-`      | Subtraction       | `x - y`  |                                       |
| `*`      | Multiplication    | `x * y`  |                                       |
| `/`      | Division          | `x / y`  | Always returns `float`                |
| `%`      | Modulus           | `x % y`  | Remainder                             |
| `**`     | Exponentiation    | `x ** y` | x to the power y                      |
| `//`     | Floor Division    | `x // y` | Rounds down to nearest integer        |

### 9.3 Operator Precedence Table (Highest → Lowest)

| Priority | Operator(s)                          | Description                       |
|----------|--------------------------------------|-----------------------------------|
| 1        | `()`                                 | Parentheses (grouping)            |
| 2        | `**`                                 | Exponentiation                    |
| 3        | `+x`, `-x`, `~x`                    | Unary plus, minus, bitwise NOT    |
| 4        | `*`, `/`, `//`, `%`                  | Multiplicative                    |
| 5        | `+`, `-`                             | Additive                          |
| 6        | `<<`, `>>`                           | Bitwise shifts                    |
| 7        | `&`                                  | Bitwise AND                       |
| 8        | `^`                                  | Bitwise XOR                       |
| 9        | `\|`                                 | Bitwise OR                        |
| 10       | `<`, `<=`, `>`, `>=`, `!=`, `==`, `in`, `not in`, `is`, `is not` | Comparisons |
| 11       | `not`                                | Logical NOT                       |
| 12       | `and`                                | Logical AND                       |
| 13       | `or`                                 | Logical OR                        |
| 14       | `if ... else`                        | Conditional expression            |
| 15       | `lambda`                             | Lambda expression                 |
| 16       | `:=`                                 | Walrus operator                   |

### 9.4 Associativity

- **Left to Right** (default for most operators)
  ```python
  # Multiplication and floor division have same precedence
  # Left one is evaluated first
  result = 20 // 3 * 2    # (20 // 3) * 2 = 6 * 2 = 12
  result = 18 * 4 // 5    # (18 * 4) // 5 = 72 // 5 = 14
  ```

- **Right to Left** (exception: `**` exponentiation)
  ```python
  result = 2 ** 3 ** 2    # 2 ** (3 ** 2) = 2 ** 9 = 512
  ```

- **Parentheses override** all precedence and associativity:
  ```python
  result = 20 // (3 * 2)  # 20 // 6 = 3
  ```

### 9.5 Logical Operators (Short-circuit Evaluation)

| Operator | Description                                | Example             |
|----------|--------------------------------------------|---------------------|
| `and`    | Returns True if **both** statements are True | `x < 5 and x < 10` |
| `or`     | Returns True if **at least one** is True     | `x < 3 or x < 4`   |
| `not`    | Reverses the boolean result                 | `not(x < 6)`        |

- `and` returns the **first falsy** value, or the **last value** if all truthy
- `or` returns the **first truthy** value, or the **last value** if all falsy

---

## 10. Input/Output — Print Formatting

### 10.1 `input()` Function
- Takes data from the user at runtime
- **Always returns a `str`**, even if the user types a number

```python
name = input("Enter your name: ")          # str
age = int(input("Enter your age: "))       # convert to int
price = float(input("Enter price: "))      # convert to float
```

| Input Type | Code           |
|------------|----------------|
| String     | `input()`      |
| Integer    | `int(input())` |
| Float      | `float(input())`|

### 10.2 F-Strings (Formatted String Literals) — Python 3.6+

The **recommended** modern way to format strings.

- **Syntax:** Prefix with `f` and use `{}` to embed expressions
- Evaluated at **runtime** — any valid Python expression inside `{}`

```python
name = "Ritika"
age = 21
print(f"Name: {name}, Age: {age}")
# Output: Name: Ritika, Age: 21

# Expressions inside braces
print(f"Sum: {10 + 20}")             # Sum: 30
print(f"Uppercase: {name.upper()}")  # Uppercase: RITIKA

# Formatting numbers
pi = 3.14159
print(f"Pi = {pi:.2f}")             # Pi = 3.14
print(f"{'Hello':>20}")             # Right-align in 20 chars
```

### 10.3 `format()` Method

An alternative to f-strings using `{}` placeholders and `.format()`.

```python
# Basic usage
print("Name: {}, Age: {}".format("Ritika", 21))

# Positional arguments
print("{0} is {1} years old".format("Ritika", 21))

# Keyword arguments
print("{name} is {age} years old".format(name="Ritika", age=21))

# Number formatting
print("Pi = {:.2f}".format(3.14159))    # Pi = 3.14
```

### 10.4 Old-Style `%` Formatting (printf-style)

Based on C's `printf()`. Considered **legacy** — replaced by f-strings and `format()`.

```python
# Basic syntax
"format_string" % value
"format_string" % (value1, value2, ...)

# Common specifiers
name = "Ritika"
age = 21
price = 99.5

print("Name: %s" % name)            # Name: Ritika
print("Age: %d" % age)              # Age: 21
print("Price: %.2f" % price)        # Price: 99.50
print("Name: %s, Age: %d" % (name, age))
```

| Specifier | Meaning   | Example          |
|-----------|-----------|------------------|
| `%s`      | String    | `"Name: %s"`     |
| `%d`      | Integer   | `"Age: %d"`      |
| `%f`      | Float     | `"Price: %f"`    |
| `%c`      | Character | `"Letter: %c"`   |

- **Advantages:** Familiar to C programmers; still in legacy systems
- **Disadvantages:** Less readable, error-prone, slower than f-strings — **not recommended for new code**

---

## 11. Command-Line Arguments Using `sys.argv`

`sys.argv` is a **list** that stores command-line arguments passed to a Python script.

- **Setup**
  ```python
  import sys
  ```

- **Structure**
  - `sys.argv[0]` → script name
  - `sys.argv[1]` → first argument
  - `sys.argv[2]` → second argument
  - `len(sys.argv)` → total count of arguments

- **Example — `greet.py`**
  ```python
  import sys
  print("Script:", sys.argv[0])
  print("First arg:", sys.argv[1])
  print("Total args:", len(sys.argv))
  ```
  Run: `python greet.py Hello World`
  ```
  Script: greet.py
  First arg: Hello
  Total args: 3
  ```

- **Important:** All arguments in `sys.argv` are **strings** — cast them manually:
  ```python
  num1 = int(sys.argv[1])
  num2 = int(sys.argv[2])
  print("Sum:", num1 + num2)
  ```

### 11.1 Using `argparse` (Bonus — from PPT)

The `argparse` module provides a more robust way to handle command-line arguments.

```python
import argparse

parser = argparse.ArgumentParser(description="Add two numbers")
parser.add_argument("num1", type=int, help="First number")
parser.add_argument("num2", type=int, help="Second number")
args = parser.parse_args()

print("Sum:", args.num1 + args.num2)
```
- Automatically handles errors
- Generates help messages (`--help`)
- Converts data types automatically

---

## 12. Control Flow

### 12.1 `if` Statement

```python
if condition:
    # runs if condition is True
```
```python
x = 10
if x > 5:
    print("x is greater than 5")
```
> **Note:** The colon `:` after the condition is **mandatory**.

### 12.2 `if-else` Statement

```python
if condition:
    # runs if True
else:
    # runs if False
```
```python
age = 18
if age >= 18:
    print("Adult")
else:
    print("Minor")
```

### 12.3 `if-elif-else` Statement

```python
if condition1:
    # runs if condition1 is True
elif condition2:
    # runs if condition1 is False and condition2 is True
else:
    # runs if all conditions above are False
```

- Conditions are checked **top to bottom**
- The **first** condition that is `True` runs its block
- If **none** are `True`, the `else` block runs
- `elif` is short for "else if" — avoids excessive indentation

```python
marks = 85
if marks >= 90:
    print("Grade: A")
elif marks >= 75:
    print("Grade: B")
elif marks >= 60:
    print("Grade: C")
else:
    print("Grade: D")
# Output: Grade: B
```

---

## 13. Match Statement (PEP 634) — Python 3.10+

**Structural pattern matching** using `match`/`case`. Similar to `switch-case` in other languages, but far more powerful.

### 13.1 Basic Syntax

```python
match value:
    case pattern1:
        # code if pattern1 matches
    case pattern2:
        # code if pattern2 matches
    case _:
        # default (like else) — if no case matches
```

- `_` is a **wildcard pattern** — always matches (acts as default)
- `match` and `case` are **soft keywords** — can be used as variable names elsewhere

### 13.2 Literal Matching

```python
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"
```

### 13.3 Combining Patterns with `|` (OR)

```python
case 401 | 403 | 404:
    return "Not allowed"
```

### 13.4 Capturing Variables (Sequence Unpacking)

```python
# point is an (x, y) tuple
match point:
    case (0, 0):
        print("Origin")
    case (0, y):
        print(f"Y={y}")
    case (x, 0):
        print(f"X={x}")
    case (x, y):
        print(f"X={x}, Y={y}")
    case _:
        raise ValueError("Not a point")
```

### 13.5 Class Patterns

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

match point:
    case Point(x=0, y=0):
        print("Origin")
    case Point(x=0, y=y):
        print(f"Y={y}")
    case Point(x=x, y=0):
        print(f"X={x}")
    case Point():
        print("Somewhere else")
    case _:
        print("Not a point")
```

### 13.6 Guards (`if` clause)

```python
match point:
    case Point(x, y) if x == y:
        print(f"On diagonal at {x}")
    case Point(x, y):
        print(f"Not on the diagonal")
```

### 13.7 Key Features Summary

- Patterns can match **literals, sequences, mappings, classes**
- Supports **nested patterns** and **variable capture**
- Supports **`|`** (OR) to combine patterns
- Supports **`as`** keyword to bind matched value
- Supports **extended unpacking**: `[x, y, *rest]`
- Mapping patterns ignore extra keys: `{"key": value}` matches even if dict has more keys
- Named constants require **dotted name** (e.g., `Color.RED`) to avoid being treated as capture variables
- See **PEP 634** (spec), **PEP 635** (motivation), **PEP 636** (tutorial) for full details

---

## 14. Loops

### 14.1 `for` Loop

An **entry-controlled** iteration statement used to iterate over a **sequence** (list, tuple, string, range, etc.).

```python
# Syntax
for variable in iterable:
    statements
```

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# Iterating over a string
for char in "Python":
    print(char)
```

### 14.2 `while` Loop

Executes a block of statements **repeatedly** until the condition becomes `False`.

```python
# Syntax
while condition:
    statement(s)
```

```python
i = 1
while i <= 5:
    print(i)
    i += 1
```

- **Infinite loop:** If the condition **never** becomes `False`, the loop runs forever
  ```python
  while True:
      print("Hello")   # runs forever — Ctrl+C to stop
  ```

### 14.3 `break` Statement

**Exits** the innermost enclosing loop immediately.

```python
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(f"{n} equals {x} * {n//x}")
            break
```

### 14.4 `continue` Statement

**Skips** the rest of the current iteration and moves to the **next** iteration.

```python
for num in range(2, 10):
    if num % 2 == 0:
        print(f"Found an even number {num}")
        continue
    print(f"Found an odd number {num}")
```

### 14.5 `else` with Loops

The `else` clause executes when the loop completes **without** encountering a `break`.

- In a `for` loop: `else` runs after the **final iteration**
- In a `while` loop: `else` runs when the condition becomes **False**
- If `break` is executed, the `else` clause is **skipped**

```python
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(n, "equals", x, "*", n // x)
            break
    else:
        # loop fell through without finding a factor
        print(n, "is a prime number")
```
Output:
```
2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
```

> **Tip:** Think of `else` with loops as: "if the loop completes normally (no `break`), then run this."

### 14.6 `pass` Statement

A **null statement** — used when a statement is syntactically required but no action is needed.

```python
for i in range(10):
    pass   # placeholder, do nothing

class MyEmptyClass:
    pass
```

---

## 15. Comprehensions

**Comprehensions** provide a concise, readable way to create collections from iterables.

### 15.1 List Comprehension

```python
# Syntax
[expression for item in iterable if condition]
```

```python
# Squares of 1–5
squares = [x * x for x in range(1, 6)]
# Output: [1, 4, 9, 16, 25]

# Even numbers from 0–9
even_numbers = [x for x in range(10) if x % 2 == 0]
# Output: [0, 2, 4, 6, 8]
```

**Equivalent traditional loop:**
```python
result = []
for x in range(10):
    if x % 2 == 0:
        result.append(x)
```

### 15.2 Set Comprehension

```python
# Syntax
{expression for item in iterable if condition}
```

```python
unique_squares = {x * x for x in range(-5, 6)}
# Output: {0, 1, 4, 9, 16, 25}  (no duplicates, unordered)
```

### 15.3 Dictionary Comprehension

```python
# Syntax
{key_expr: value_expr for item in iterable if condition}
```

```python
square_dict = {x: x * x for x in range(1, 6)}
# Output: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

even_square_dict = {x: x * x for x in range(10) if x % 2 == 0}
# Output: {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

### 15.4 Nested Comprehension

Used when there are **multiple loops**.

```python
# Matrix creation (3×3)
matrix = [[j for j in range(3)] for i in range(3)]
# Output: [[0, 1, 2], [0, 1, 2], [0, 1, 2]]

# Flattening a 2D list
matrix = [[1, 2], [3, 4], [5, 6]]
flattened = [num for row in matrix for num in row]
# Output: [1, 2, 3, 4, 5, 6]
```

### 15.5 Summary

| Type       | Syntax     | Returns  |
|------------|-----------|----------|
| List       | `[...]`   | `list`   |
| Set        | `{...}`   | `set`    |
| Dict       | `{k: v}`  | `dict`   |
| Generator  | `(...)`   | `generator` (lazy) |

---

## 16. `range()`

The built-in `range()` function generates an **immutable sequence of numbers**.

- **Syntax**
  ```python
  range(stop)               # 0 to stop-1, step=1
  range(start, stop)        # start to stop-1, step=1
  range(start, stop, step)  # start to stop-1, with given step
  ```

- **Examples**
  ```python
  list(range(5))           # [0, 1, 2, 3, 4]
  list(range(2, 8))        # [2, 3, 4, 5, 6, 7]
  list(range(0, 10, 2))    # [0, 2, 4, 6, 8]
  list(range(10, 0, -1))   # [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
  list(range(-10, -100, -30))  # [-10, -40, -70]
  ```

- **Key Points**
  - The **stop** value is **never included** in the sequence
  - Default step is `+1`
  - `range()` returns a **`range` object** (not a list) — memory efficient
  - Commonly used with `for` loops: `for i in range(5): ...`
  - Supports negative steps for counting backwards

---

## Topics NOT Found in the PPT

The following topics from the user's requested list were **not covered** in the PPT (88 slides):

| Topic | Status |
|-------|--------|
| **Iterator Protocol (`__iter__`, `__next__`)** | Not covered in the PPT (mentioned in syllabus on Page 2, but no dedicated slides) |
| **Unpacking and Zipping** | Not covered (listed in syllabus but no slides) |
| **`enumerate()`** | Not covered (listed in syllabus but no slides) |
| **`zip()`** | Not covered (listed in syllabus but no slides) |

> These topics are listed in the Unit-1 syllabus (Page 2) but do not have dedicated PPT slides. The user's instruction was to ignore topics not found in the PPT, so they are listed here for awareness but not expanded.

---

## Reference Links

These links were provided in the `Links for python topics.docx` file and are useful for further study:

- **W3Schools Python Tutorial:** https://www.w3schools.com/python/python_intro.asp
- **Python Official Tutorial:** https://docs.python.org/3/tutorial/index.html
- **GeeksforGeeks Python Tutorial:** https://www.geeksforgeeks.org/python/python-programming-language-tutorial/
- **TutorialsPoint Python:** https://www.tutorialspoint.com/python/index.htm
- **TutorialsPoint — Command-Line Arguments:** https://www.tutorialspoint.com/python/python_command_line_arguments.htm
- **Python Official — argparse:** https://docs.python.org/3/library/argparse.html
- **GeeksforGeeks — Command-Line Arguments:** https://www.geeksforgeeks.org/python/command-line-arguments-in-python/

**Additional Official References:**
- **PEP 634 — Structural Pattern Matching:** https://peps.python.org/pep-0634/
- **PEP 636 — Pattern Matching Tutorial:** https://peps.python.org/pep-0636/
- **Python Expressions & Operator Precedence:** https://docs.python.org/3/reference/expressions.html
- **Python Control Flow:** https://docs.python.org/3/tutorial/controlflow.html
- **PEP 484 — Type Hints:** https://peps.python.org/pep-0484/
- **PEP 257 — Docstring Conventions:** https://peps.python.org/pep-0257/
- **PEP 8 — Style Guide:** https://peps.python.org/pep-0008/

---

*Notes generated from PPT analysis + Python official documentation + web references.*
