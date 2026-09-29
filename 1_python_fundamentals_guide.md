# Python Fundamentals: A Complete Learning & Reference Guide

## Overview

This document is a complete, structured reference for the core building blocks of Python. It is designed so that a **beginner** can learn each concept from scratch, and an **experienced developer** can use it as a quick, accurate reference.

Each topic follows a consistent format — Definition, Purpose, Syntax, Detailed Explanation, Examples with Output, Real-World Use Cases, Important Points, Common Mistakes, and Best Practices — so you always know where to find what you need. Related topics are cross-referenced and compared so you understand not just *what* each concept is, but *when* and *why* to use it.

By the end of this guide, you will understand how Python stores and names data (literals, variables), the vocabulary Python reserves for itself (keywords), the basic building-block types (primitive datatypes), how to manipulate text (string operations), how to safely move between types (type conversion), how to compute and compare values (arithmetic, comparison, logical operators), how Python decides evaluation order (precedence and associativity), and how to communicate with a user through the console (`print()` and `input()`).

---

## Table of Contents

1. [Literals](#1-literals)
2. [Variables](#2-variables)
3. [Keywords](#3-keywords)
4. [Primitive Datatypes](#4-primitive-datatypes)
5. [Basic Operations with Strings](#5-basic-operations-with-strings)
6. [Type Conversion — int, float, str](#6-type-conversion--int-float-str)
7. [Type Conversion — bool](#7-type-conversion--bool)
8. [Arithmetic and Assignment Operators](#8-arithmetic-and-assignment-operators)
9. [Comparison and Logical Operators](#9-comparison-and-logical-operators)
10. [Associativity and Precedence of Operators](#10-associativity-and-precedence-of-operators)
11. [Printing to the Console — the print() Function](#11-printing-to-the-console--the-print-function)
12. [Taking Input from the User — the input() Function](#12-taking-input-from-the-user--the-input-function)
13. [Overall Summary](#13-overall-summary)
14. [Quick Revision / Cheat Sheet](#14-quick-revision--cheat-sheet)
15. [Common Interview Questions](#15-common-interview-questions)
16. [Practice Exercises](#16-practice-exercises)

---
## 1. Literals

### Definition

A **literal** is a fixed, raw value written directly into source code. It represents data as-is — not a variable, not an expression to be resolved, just the value itself. For example, `10`, `"hello"`, and `True` are all literals.

### Purpose / Why It Is Used

Literals are the fundamental way we introduce concrete data into a program. Every variable ultimately gets its starting value from a literal, an expression built from literals, or user input. Without literals, there would be no way to specify constant, known values in code.

### Syntax

```python
<value>
```
There is no special syntax to "declare" a literal — you simply write the value.

### Detailed Explanation

Python supports several categories of literals:

| Category | Description | Examples |
|---|---|---|
| Numeric | Integers, floats, complex numbers | `10`, `3.14`, `2+3j` |
| String | Text data | `'hi'`, `"hi"`, `'''hi'''` |
| Boolean | Truth values | `True`, `False` |
| Special | Absence of value | `None` |
| Collection | Built-in containers | `[1,2]`, `(1,2)`, `{1,2}`, `{"a":1}` |

**Numeric literal formats:**

| Format | Prefix | Example | Decimal Value |
|---|---|---|---|
| Decimal | none | `10` | 10 |
| Binary | `0b` | `0b1010` | 10 |
| Octal | `0o` | `0o12` | 10 |
| Hexadecimal | `0x` | `0xA` | 10 |
| Scientific | `e`/`E` | `1.5e2` | 150.0 |

### Examples

```python
# Numeric literals
integer_literal = 100
float_literal = 3.14
complex_literal = 2 + 3j
binary_literal = 0b1010
octal_literal = 0o12
hex_literal = 0xA

print(integer_literal, float_literal, complex_literal)
print(binary_literal, octal_literal, hex_literal)
```

Output:
```
100 3.14 (2+3j)
10 10 10
```

```python
# Underscores improve readability in large numbers (Python 3.6+)
population = 1_400_000_000
print(population)
```

Output:
```
1400000000
```

```python
# String literals
single = 'Hello'
double = "World"
triple = '''This spans
multiple lines'''
raw = r"C:\Users\name"

print(single, double)
print(triple)
print(raw)
```

Output:
```
Hello World
This spans
multiple lines
C:\Users\name
```

```python
# Boolean, None, and collection literals
is_valid = True
result = None
nums = [1, 2, 3]
coords = (4, 5)
unique = {1, 2, 3}
person = {"name": "Sam", "age": 30}

print(is_valid, result, nums, coords, unique, person)
```

Output:
```
True None [1, 2, 3] (4, 5) {1, 2, 3} {'name': 'Sam', 'age': 30}
```

### Real-World Use Cases

- Setting configuration constants: `MAX_RETRIES = 5`
- Defining initial/default values: `balance = 0.0`
- Embedding fixed text like messages or labels: `WELCOME_MSG = "Welcome!"`
- Representing lookup or config data directly: `STATUS_CODES = {200: "OK", 404: "Not Found"}`

### Important Points / Rules

- Leading zeros are **not allowed** in decimal integer literals (`007` is a `SyntaxError`).
- Underscores in numeric literals cannot be leading, trailing, or consecutive (`1__000` is invalid).
- Float literals may omit a leading or trailing digit: `.5` equals `0.5`, `5.` equals `5.0`.
- Adjacent string literals are automatically concatenated at compile time: `"Hello " "World"` becomes `"Hello World"`.
- Raw strings (`r"..."`) disable escape sequence processing — useful for regex patterns and file paths.

### Common Mistakes

```python
# Mistake 1: Leading zero in decimal literal
# num = 007          # ❌ SyntaxError

# Mistake 2: Bad underscore placement
# x = 1000_          # ❌ SyntaxError
# x = _1000          # This is NOT a literal — it's parsed as a variable name

# Mistake 3: Forgetting raw string for paths, causing broken escapes
path = "C:\newFolder"    # ⚠️ \n is interpreted as newline! Not what you want.
print(path)
```

Output:
```
C:
ewFolder
```

```python
# Fix: use a raw string
path = r"C:\newFolder"
print(path)
```

Output:
```
C:\newFolder
```

### Best Practices

> **Tip:** Use underscores (`1_000_000`) in long numeric literals to improve readability.

> **Tip:** Always use raw strings (`r"..."`) for Windows file paths and regular expressions to avoid unintended escape sequences.

> **Warning:** Don't rely on adjacent string literal concatenation for long strings spread across many lines — prefer explicit `+` or parentheses with clear formatting for readability.

### Key Takeaways

- A literal is a fixed value written directly in code.
- Python has numeric, string, boolean, `None`, and collection literals.
- Numeric literals support binary, octal, hex, and scientific notation.
- Underscore separators and raw strings are small but important quality-of-life features.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 2. Variables

### Definition

A **variable** is a named reference bound to an object stored in memory. In Python, a variable does not "contain" a value the way a box contains an item — rather, it is a **label pointing to an object**. Python is **dynamically typed**: you don't declare a type, and a variable can be rebound to a value of a different type at any time.

### Purpose / Why It Is Used

Variables let a program store, retrieve, and manipulate data using meaningful names instead of hardcoded literals scattered throughout the code. They make programs readable, reusable, and maintainable.

### Syntax

```python
variable_name = value
```

### Detailed Explanation

When you write `x = 10`, Python:
1. Creates an integer object `10` in memory.
2. Binds the name `x` to that object.

If you later write `x = "hello"`, Python creates a new string object and rebinds `x` to it — the old integer object is discarded (garbage collected) if nothing else references it. This is different from statically typed languages, where a variable's type is fixed at declaration.

**Naming rules:**

| Rule | Valid Example | Invalid Example |
|---|---|---|
| Must start with a letter or underscore | `_name`, `age1` | `1age` ❌ |
| Can contain letters, digits, underscores | `first_name2` | `first-name` ❌ |
| Case-sensitive | `Age` ≠ `age` | — |
| Cannot be a reserved keyword | `total` | `class` ❌ |
| No spaces allowed | `user_name` | `user name` ❌ |

### Examples

```python
# Basic assignment
name = "Alice"
age = 25
height = 5.6
print(name, age, height)
```

Output:
```
Alice 25 5.6
```

```python
# Multiple assignment - same value
x = y = z = 0
print(x, y, z)
```

Output:
```
0 0 0
```

```python
# Multiple assignment - different values
a, b, c = 1, 2, 3
print(a, b, c)
```

Output:
```
1 2 3
```

```python
# Swapping without a temporary variable
a, b = 10, 20
a, b = b, a
print(a, b)
```

Output:
```
20 10
```

```python
# Dynamic typing — reassigning to a different type
val = 10
print(type(val))
val = "now a string"
print(type(val))
val = [1, 2, 3]
print(type(val))
```

Output:
```
<class 'int'>
<class 'str'>
<class 'list'>
```

```python
# Extended unpacking with *
first, *middle, last = [1, 2, 3, 4, 5]
print(first, middle, last)
```

Output:
```
1 [2, 3, 4] 5
```

### Real-World Use Cases

- Storing user-provided data: `username = input("Enter username: ")`
- Holding running totals or counters: `total = 0`
- Referencing configuration and state across a program: `is_logged_in = False`
- Assigning meaningful names to computed intermediate results for readability.

### Important Points / Rules

- Variables are case-sensitive: `Age` and `age` are different variables.
- Python has **no true constants** — uppercase names like `PI = 3.14` are a convention, not enforced immutability.
- Assignment to mutable objects (lists, dicts, sets) shares the same underlying object unless explicitly copied.
- Assignment to immutable objects (int, float, str, tuple) never affects other variables referencing the "same" value.
- Use `global` inside a function to modify a variable defined outside it; use `nonlocal` for enclosing (non-global) scopes.

### Common Mistakes

```python
# Mistake 1: Using a variable before assigning it
# print(score)          # ❌ NameError: name 'score' is not defined

# Mistake 2: Assuming lists behave like immutable values on assignment
list1 = [1, 2, 3]
list2 = list1              # NOT a copy — same object
list2.append(4)
print(list1)                # ⚠️ [1, 2, 3, 4] — list1 changed too!
```

Output:
```
[1, 2, 3, 4]
```

```python
# Fix: use .copy() or list() to create an independent copy
list1 = [1, 2, 3]
list2 = list1.copy()
list2.append(4)
print(list1, list2)
```

Output:
```
[1, 2, 3] [1, 2, 3, 4]
```

```python
# Mistake 3: Forgetting 'global' when modifying a global variable inside a function
counter = 0

def increment():
    counter += 1     # ❌ UnboundLocalError: local variable 'counter' referenced before assignment

# increment()
```

```python
# Fix
counter = 0

def increment():
    global counter
    counter += 1

increment()
print(counter)
```

Output:
```
1
```

### Best Practices

> **Tip:** Use descriptive, lowercase, underscore-separated names (`user_age`, not `ua` or `UserAge`) — this is PEP 8 convention.

> **Tip:** Use UPPERCASE names for values intended to act as constants (`MAX_LIMIT = 100`), even though Python won't enforce immutability.

> **Warning:** Be careful when assigning mutable objects (lists, dicts) to a new variable — you get a second reference to the *same* object, not an independent copy.

### Comparison: Mutable vs Immutable Assignment

| Aspect | Immutable (int, str, tuple) | Mutable (list, dict, set) |
|---|---|---|
| Reassignment | Creates a new object | Same object, in-place changes possible |
| `b = a` then modify `b` | `a` is unaffected | `a` is also affected (same object) |
| Safe to share across functions? | Yes | Only if changes are intentional |

### Key Takeaways

- A variable is a name bound to an object; Python is dynamically typed.
- Reassignment to immutable types creates a new object; mutable types can be shared and mutated in place.
- Python naming rules are strict about starting characters, keywords, and spacing.
- `global`/`nonlocal` are needed to modify variables from outer scopes inside functions.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 3. Keywords

### Definition

**Keywords** are reserved words that form part of Python's syntax and grammar. They have fixed, special meaning to the interpreter and **cannot** be used as identifiers (variable names, function names, class names).

### Purpose / Why It Is Used

Keywords let Python recognize the structural elements of a program — conditionals, loops, function/class definitions, exception handling, and so on. Reserving them prevents ambiguity between "instructions to the interpreter" and "names chosen by the programmer."

### Syntax

Keywords are used as-is, exactly as spelled, in their designated grammatical positions (e.g., `if condition:`, `def function_name():`).

### Detailed Explanation

You can programmatically list all current keywords:

```python
import keyword
print(keyword.kwlist)
```

Output (Python 3.12+, 35 keywords):
```
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

**Categorized keyword reference:**

| Category | Keywords | Purpose |
|---|---|---|
| Value keywords | `True`, `False`, `None` | Represent fixed built-in values |
| Logical/membership | `and`, `or`, `not`, `is`, `in` | Boolean logic and membership tests |
| Control flow | `if`, `elif`, `else`, `for`, `while`, `break`, `continue`, `pass` | Branching and looping |
| Functions/classes | `def`, `return`, `class`, `lambda`, `yield` | Define reusable code and generators |
| Exceptions | `try`, `except`, `finally`, `raise`, `assert` | Error handling |
| Scope | `global`, `nonlocal` | Control variable scope resolution |
| Import | `import`, `from`, `as` | Bring in external modules |
| Async | `async`, `await` | Asynchronous programming |
| Context managers | `with` | Resource management (files, locks) |
| Deletion | `del` | Remove a name/reference |

**Soft keywords** (Python 3.10+) are only special in specific contexts and can otherwise be used as normal identifiers:

```python
import keyword
print(keyword.softkwlist)
```

Output:
```
['_', 'case', 'match', 'type']
```

### Examples

```python
# Checking if a word is a keyword
import keyword
print(keyword.iskeyword("class"))   # True
print(keyword.iskeyword("Class"))   # False (case-sensitive)
print(keyword.iskeyword("match"))   # False — it's a SOFT keyword
```

Output:
```
True
False
False
```

```python
# Soft keywords can be used as normal variable names outside their special context
match = "this works fine"
type = "also works, but shadows the built-in type() function"
print(match)
print(type)
```

Output:
```
this works fine
also works, but shadows the built-in type() function
```

```python
# match statement — the actual special-context use of 'match'/'case' (Python 3.10+)
value = 2
match value:
    case 1:
        print("one")
    case 2:
        print("two")
    case _:
        print("other")
```

Output:
```
two
```

### Real-World Use Cases

- `if`/`elif`/`else` — decision-making logic in almost every program.
- `try`/`except`/`finally` — robust error handling for file I/O, network calls, user input.
- `with` — safely opening/closing files or database connections.
- `import`/`from`/`as` — organizing code across modules and using third-party libraries.
- `class`/`def` — structuring object-oriented and reusable functional code.

### Important Points / Rules

- Keywords **cannot** be assigned to, reassigned, or used as function/class/variable names — doing so raises a `SyntaxError`.
- Keyword checks are **case-sensitive**: `True` is a keyword, `true` is not.
- Soft keywords (`match`, `case`, `_`, `type`) are only reserved in their specific grammatical context.
- Built-in function names like `print`, `len`, `type` are **not** keywords — they *can* technically be reassigned (though doing so is bad practice).

### Common Mistakes

```python
# Mistake 1: Using a keyword as a variable name
# True = 5             # ❌ SyntaxError: cannot assign to True
# def = "test"         # ❌ SyntaxError: invalid syntax

# Mistake 2: Confusing built-ins with keywords
print = "oops"          # ⚠️ Legal! print is a built-in, NOT a keyword
# print("test")         # ❌ TypeError: 'str' object is not callable
del print                 # restores access to the print() function
print("restored")
```

Output:
```
restored
```

### Best Practices

> **Warning:** Even though built-in function names (`print`, `list`, `type`, `id`) aren't keywords and *can* be reassigned, avoid doing so — it silently breaks their normal behavior elsewhere in your code.

> **Tip:** If you get an unexpected `SyntaxError` on what looks like a normal assignment, check whether you accidentally used a keyword as a variable name.

> **Tip:** Use `keyword.iskeyword("word")` when writing tools that need to validate user-supplied identifiers (e.g., a code generator).

### Comparison: Keywords vs Built-in Functions vs Soft Keywords

| Aspect | Keywords (`if`, `class`) | Built-ins (`print`, `len`) | Soft Keywords (`match`, `type`) |
|---|---|---|---|
| Reserved everywhere? | Yes | No | Only in specific syntax context |
| Can be reassigned? | No (`SyntaxError`) | Yes (not recommended) | Yes, outside their special context |
| Found in `keyword.kwlist`? | Yes | No | No (in `keyword.softkwlist`) |

### Key Takeaways

- Keywords are reserved words that define Python's syntax and can never be used as identifiers.
- Python 3.12 has 35 keywords, checkable via `keyword.kwlist`.
- Soft keywords (`match`, `case`, `_`, `type`) are context-sensitive, not globally reserved.
- Built-in function names are not keywords and are technically reassignable — but shouldn't be.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 4. Primitive Datatypes

### Definition

Python's **primitive (scalar) datatypes** are the basic built-in types that represent single, indivisible values: `int`, `float`, `complex`, `str`, `bool`, and `NoneType`. Technically, everything in Python is an object (there's no true "primitive" distinct from objects, unlike Java or C), but these types are conventionally treated as the fundamental building blocks.

### Purpose / Why It Is Used

These types form the foundation for representing numbers, text, truth values, and "nothingness" in any Python program. Every more complex data structure (lists, dicts, custom classes) is ultimately built from combinations of these basic types.

### Syntax

```python
value = <literal>          # type is inferred automatically
type(value)                  # check the type at runtime
```

### Detailed Explanation

| Type | Description | Example | Mutable? |
|---|---|---|---|
| `int` | Whole numbers, arbitrary precision | `42`, `-7` | No |
| `float` | Decimal numbers (IEEE 754 double) | `3.14`, `-0.5` | No |
| `complex` | Numbers with real & imaginary parts | `3+4j` | No |
| `str` | Sequence of Unicode characters | `"hello"` | No |
| `bool` | Truth value (subclass of `int`) | `True`, `False` | No |
| `NoneType` | Represents absence of a value | `None` | No |

### Examples

```python
a = 42
f = 3.14159
c = 3 + 4j
s = "Hello"
b = True
n = None

for val in (a, f, c, s, b, n):
    print(val, "->", type(val))
```

Output:
```
42 -> <class 'int'>
3.14159 -> <class 'float'>
(3+4j) -> <class 'complex'>
Hello -> <class 'str'>
True -> <class 'bool'>
None -> <class 'NoneType'>
```

```python
# int has arbitrary precision - no overflow
huge = 10 ** 100
print(huge)
```

Output:
```
100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
```

```python
# bool is a SUBCLASS of int
print(isinstance(True, int))     # True
print(True + True)                 # 2
print(True == 1)                   # True
```

Output:
```
True
2
True
```

```python
# Special float values
print(float('inf'))
print(float('-inf'))
print(float('nan'))
```

Output:
```
inf
-inf
nan
```

### Real-World Use Cases

- `int` — counters, indices, IDs, quantities.
- `float` — measurements, prices, scientific calculations, percentages.
- `complex` — signal processing, electrical engineering, scientific computing.
- `str` — names, messages, file paths, all text-based data.
- `bool` — flags, conditions, feature toggles (`is_active`, `has_permission`).
- `None` — default/sentinel value for "not yet set" or "no result".

### Important Points / Rules

- Python integers have **no fixed size** and cannot overflow (unlike C's `int32`/`int64`).
- Floating-point numbers follow IEEE 754 and are subject to **precision errors** (`0.1 + 0.2 != 0.3`).
- `bool` is a subtype of `int`; `True` behaves as `1` and `False` as `0` in arithmetic.
- `None` is a **singleton** — always compare using `is None`, not `== None`.
- Division `/` always returns a `float`, even for two integers with no remainder.

### Common Mistakes

```python
# Mistake 1: Comparing floats directly for equality
print(0.1 + 0.2 == 0.3)          # ⚠️ False due to floating-point precision
```

Output:
```
False
```

```python
# Fix: use math.isclose() for float comparisons
import math
print(math.isclose(0.1 + 0.2, 0.3))
```

Output:
```
True
```

```python
# Mistake 2: Using == to compare with None
x = None
print(x == None)     # ⚠️ Works, but not Pythonic
print(x is None)      # ✅ Correct, idiomatic approach
```

Output:
```
True
True
```

```python
# Mistake 3: Assuming NaN equals itself
nan = float('nan')
print(nan == nan)      # ⚠️ False! NaN is never equal to anything, including itself
```

Output:
```
False
```

### Best Practices

> **Tip:** Always use `math.isclose()` (or round to a fixed number of decimals) when comparing floats.

> **Tip:** Use `is None` / `is not None` for `None` checks — it's both idiomatic and faster than `==`.

> **Warning:** Don't rely on `int is int` identity comparisons for large numbers — CPython only caches small integers (-5 to 256) as singletons; this is an implementation detail, not a guaranteed language feature.

### Comparison: int vs float vs complex

| Feature | `int` | `float` | `complex` |
|---|---|---|---|
| Precision | Arbitrary (exact) | ~15-17 significant digits | Same as float, per component |
| Supports `<`, `>` | Yes | Yes | No (`TypeError`) |
| Can represent fractions? | No | Yes | Yes (with imaginary part) |
| Common use | Counting, indexing | Measurements, division results | Scientific/engineering math |

### Key Takeaways

- Python's six primitive-like types are `int`, `float`, `complex`, `str`, `bool`, `NoneType`.
- Integers never overflow; floats can lose precision.
- `bool` is technically an `int` subclass — `True`/`False` participate in arithmetic.
- Always compare `None` with `is`, and floats with `math.isclose()`.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 5. Basic Operations with Strings

### Definition

A **string** (`str`) is an immutable, ordered sequence of Unicode characters, used to represent text. "Immutable" means once a string is created, its content cannot be changed in place — any modification creates a new string object.

### Purpose / Why It Is Used

Strings are used anywhere text is involved: names, messages, file content, user input, formatted output, and more. Python provides a rich set of built-in operations and methods for creating, combining, inspecting, and transforming strings.

### Syntax

```python
"double-quoted string"
'single-quoted string'
'''triple-quoted
multi-line string'''
f"formatted {expression} string"
```

### Detailed Explanation

#### 5.1 Creating and Combining Strings

```python
s = "Hello, World!"

# Concatenation with +
greeting = "Hello" + " " + "World"

# Repetition with *
line = "-" * 20

print(greeting)
print(line)
```

Output:
```
Hello World
--------------------
```

#### 5.2 Indexing and Slicing

```python
s = "Hello, World!"
print(s[0])        # first character
print(s[-1])        # last character
print(s[0:5])        # slice: "Hello"
print(s[7:])          # slice: "World!"
print(s[::-1])          # reversed string
print(s[::2])            # every 2nd character
```

Output:
```
H
!
Hello
World!
!dlroW ,olleH
Hlo ol!
```

#### 5.3 Length and Membership

```python
s = "Hello, World!"
print(len(s))
print("World" in s)
print("world" in s)     # case-sensitive!
```

Output:
```
13
True
False
```

#### 5.4 Common String Methods

| Method | Purpose | Example | Result |
|---|---|---|---|
| `.upper()` | Convert to uppercase | `"hi".upper()` | `'HI'` |
| `.lower()` | Convert to lowercase | `"HI".lower()` | `'hi'` |
| `.strip()` | Remove leading/trailing whitespace | `"  hi  ".strip()` | `'hi'` |
| `.replace(a,b)` | Replace substring | `"hi".replace("h","H")` | `'Hi'` |
| `.split(sep)` | Split into a list | `"a,b".split(",")` | `['a','b']` |
| `.join(iterable)` | Join list into string | `"-".join(["a","b"])` | `'a-b'` |
| `.find(sub)` | Index of substring (-1 if absent) | `"hi".find("i")` | `1` |
| `.count(sub)` | Count occurrences | `"hihi".count("hi")` | `2` |
| `.startswith(x)` | Check prefix | `"hi".startswith("h")` | `True` |
| `.endswith(x)` | Check suffix | `"hi".endswith("i")` | `True` |

```python
s = "  Hello, World!  "
print(s.upper())
print(s.lower())
print(s.strip())
print(s.replace("World", "Python"))
print(s.strip().split(","))
print(" ".join(["a", "b", "c"]))
print(s.find("World"))
print(s.count("l"))
```

Output:
```
  HELLO, WORLD!  
  hello, world!  
Hello, World!
  Hello, Python!  
['Hello', ' World!  ']
a b c
9
3
```

#### 5.5 String Formatting

```python
name = "Alice"
age = 30

# f-strings (Python 3.6+, preferred)
print(f"{name} is {age} years old")
print(f"{3.14159:.2f}")           # rounds to 2 decimal places

# .format() method
print("{} is {} years old".format(name, age))
print("{0} - {1} - {0}".format("a", "b"))

# % formatting (legacy style)
print("%s is %d years old" % (name, age))
```

Output:
```
Alice is 30 years old
3.14
Alice is 30 years old
a - b - a
Alice is 30 years old
```

### Real-World Use Cases

- Parsing and cleaning user input (`.strip()`, `.lower()`)
- Building dynamic messages/emails (f-strings)
- Splitting CSV-like data (`.split(",")`)
- Validating text formats (`.startswith()`, `.isdigit()`)
- Constructing file paths and URLs

### Important Points / Rules

- Strings are **immutable** — every "modifying" method returns a *new* string.
- Indexing is 0-based; negative indices count from the end.
- Slicing never raises `IndexError`, even with out-of-range bounds.
- String comparison is **lexicographic** based on Unicode code points, not numeric value.
- `.split()` with no argument splits on any whitespace and removes empty strings; `.split(" ")` splits strictly on single spaces and keeps empties.

### Common Mistakes

```python
# Mistake 1: Trying to modify a string in place
s = "hello"
# s[0] = "H"      # ❌ TypeError: 'str' object does not support item assignment
s = "H" + s[1:]    # ✅ correct approach: build a new string
print(s)
```

Output:
```
Hello
```

```python
# Mistake 2: Concatenating a string with a non-string directly
age = 25
# msg = "Age: " + age     # ❌ TypeError: can only concatenate str (not "int") to str
msg = "Age: " + str(age)   # ✅ convert explicitly
print(msg)
```

Output:
```
Age: 25
```

```python
# Mistake 3: Comparing numeric-looking strings as if they were numbers
print("10" < "9")     # ⚠️ True! This is LEXICOGRAPHIC comparison, not numeric
print(int("10") < int("9"))   # ✅ False, correct numeric comparison
```

Output:
```
True
False
```

### Best Practices

> **Tip:** Prefer f-strings for formatting — they are the most readable and performant option in modern Python.

> **Tip:** Use `.strip()` on user input before validation or comparison to avoid whitespace-related bugs.

> **Warning:** Never assume `.split()` with no arguments behaves the same as `.split(" ")` — they treat consecutive/leading/trailing whitespace differently.

### Comparison: String Formatting Methods

| Method | Introduced | Readability | Recommended |
|---|---|---|---|
| `%` formatting | Python 1.x | Low | Legacy code only |
| `.format()` | Python 2.6+ | Medium | When f-strings unavailable |
| f-strings | Python 3.6+ | High | ✅ Preferred for new code |

### Key Takeaways

- Strings are immutable sequences of Unicode characters supporting indexing, slicing, and a rich method set.
- f-strings are the modern, preferred way to format strings.
- String comparisons are lexicographic, not numeric — convert to `int`/`float` before comparing numeric text.
- `.split()` behavior changes significantly depending on whether a separator argument is given.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 6. Type Conversion — int, float, str

### Definition

**Type conversion** (or type casting) is converting a value from one datatype to another. Python supports **implicit conversion** (automatic, performed by the interpreter) and **explicit conversion** (manual, using functions like `int()`, `float()`, `str()`).

### Purpose / Why It Is Used

Data doesn't always arrive in the type you need — user input is always text, calculations may mix int/float, and output often needs to be a string. Type conversion functions let you move data between types safely and predictably.

### Syntax

```python
int(value)      # convert to integer
float(value)    # convert to float
str(value)      # convert to string
```

### Detailed Explanation

#### 6.1 Implicit Conversion (Type Coercion)

Python automatically converts (promotes) types in mixed-type arithmetic when it's safe to do so — typically `int` → `float`.

```python
result = 5 + 2.5          # int + float
print(result, type(result))
```

Output:
```
7.5 <class 'float'>
```

#### 6.2 Explicit Conversion

```python
# int()
print(int("42"))      # from string
print(int(3.99))       # from float -- TRUNCATES, does not round
print(int(-3.99))       # truncates toward zero
print(int(True))         # from bool

# float()
print(float("3.14"))
print(float(10))
print(float(True))

# str()
print(str(42))
print(str(3.14))
print(str([1, 2, 3]))
```

Output:
```
42
3
-3
1
3.14
10.0
1.0
42
3.14
[1, 2, 3]
```

#### 6.3 int() with a Base Argument

```python
print(int("1010", 2))     # binary string to int
print(int("FF", 16))       # hex string to int
print(int("17", 8))         # octal string to int
```

Output:
```
10
255
15
```

### Real-World Use Cases

- Converting `input()` text into numbers for calculations: `age = int(input("Age: "))`
- Formatting numeric results as strings for display: `"Total: " + str(total)`
- Parsing numeric data from files or APIs (always read as text first).
- Converting between number bases (binary/hex/octal) for low-level or networking tasks.

### Important Points / Rules

- `int()` **truncates** toward zero for floats — it does **not** round.
- `int()` cannot parse a decimal-looking string directly (`int("3.14")` fails) — convert via `float()` first.
- `int()` strips leading/trailing whitespace from strings, but not internal whitespace.
- `str()` works on virtually any object and never raises an error for standard types.
- Converting `None` or `complex` to `int`/`float` raises `TypeError`.

### Common Mistakes

```python
# Mistake 1: Expecting int() to round
print(int(3.7))     # ⚠️ 3, NOT 4
print(int(-3.7))     # ⚠️ -3, NOT -4

# Fix: use round() for actual rounding
print(round(3.7))
print(round(-3.7))
```

Output:
```
3
-3
4
-4
```

```python
# Mistake 2: Converting a decimal string directly with int()
try:
    int("3.14")
except ValueError as e:
    print("Error:", e)

# Fix: convert via float() first
print(int(float("3.14")))
```

Output:
```
Error: invalid literal for int() with base 10: '3.14'
3
```

```python
# Mistake 3: Converting non-numeric text
try:
    int("hello")
except ValueError as e:
    print("Error:", e)
```

Output:
```
Error: invalid literal for int() with base 10: 'hello'
```

```python
# Mistake 4: Converting None
try:
    int(None)
except TypeError as e:
    print("Error:", e)
```

Output:
```
Error: int() argument must be a string, a bytes-like object or a real number, not 'NoneType'
```

### Best Practices

> **Tip:** Always wrap `int()`/`float()` conversions of user input in a `try`/`except ValueError` block.

> **Tip:** Use `round()` when you need rounding behavior — never assume `int()` rounds.

> **Warning:** `str(0.1 + 0.2)` will show `'0.30000000000000004'` — floating point precision issues are visible even after string conversion.

### Comparison: int() vs float() vs str()

| Function | Input Accepted | Common Failure | Typical Use |
|---|---|---|---|
| `int()` | int-like strings, floats (truncates), bool | decimal strings, `None`, `complex` | Whole number data, indices, counts |
| `float()` | numeric strings (incl. `"inf"`, `"nan"`), int, bool | non-numeric strings, `None` | Measurements, division results |
| `str()` | virtually anything | (rarely fails) | Display, concatenation, logging |

### Key Takeaways

- `int()`, `float()`, and `str()` explicitly convert between types; Python also implicitly promotes `int` to `float` in mixed arithmetic.
- `int()` truncates rather than rounds — use `round()` for rounding.
- Convert decimal strings to `int` via `float()` first.
- Always handle `ValueError`/`TypeError` when converting untrusted input.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 7. Type Conversion — bool

### Definition

`bool()` converts any value into `True` or `False` based on Python's **truthiness** rules. Every object in Python has an inherent boolean interpretation used implicitly in conditions like `if`, `while`, and logical operators.

### Purpose / Why It Is Used

Truthiness lets you write concise conditional checks (`if my_list:` instead of `if len(my_list) > 0:`) and lets custom objects define their own "emptiness" or "validity" semantics via `__bool__`/`__len__`.

### Syntax

```python
bool(value)
```

### Detailed Explanation

**Falsy values** in Python (everything else is truthy):

| Category | Falsy Value(s) |
|---|---|
| Numbers | `0`, `0.0`, `0j` |
| Strings | `""` (empty string only) |
| Collections | `[]`, `()`, `{}`, `set()`, `range(0)` |
| Special | `None` |
| Custom objects | Only if `__bool__` returns `False` or `__len__` returns `0` |

```python
print(bool(0), bool(1), bool(-1))
print(bool(""), bool("False"), bool(" "))
print(bool([]), bool([0]), bool({}), bool(()))
print(bool(None))
```

Output:
```
False True True
False True True
False True False False
False
```

### Real-World Use Cases

- Checking if a collection has data: `if user_list:` instead of `if len(user_list) > 0:`
- Validating non-empty user input: `if username.strip():`
- Feature flags: `if is_enabled:`
- Custom object validity checks via `__bool__`.

### Important Points / Rules

- A **non-empty string is always truthy**, even `"False"`, `"0"`, or `" "` — a very common beginner trap.
- `bool` is a subclass of `int`; `True == 1` and `False == 0`.
- `float('nan')` is truthy, unlike some other languages' NaN handling.
- Custom classes are truthy by default unless they define `__bool__` or `__len__`.

### Examples

```python
# The classic trap: non-empty string is always truthy
if bool("False"):
    print("This runs!")     # runs, because "False" is a non-empty string
```

Output:
```
This runs!
```

```python
# Custom __bool__ controls truthiness
class Wallet:
    def __init__(self, balance):
        self.balance = balance
    def __bool__(self):
        return self.balance > 0

w1 = Wallet(100)
w2 = Wallet(0)
print(bool(w1), bool(w2))
```

Output:
```
True False
```

```python
# __len__ as a fallback for truthiness when __bool__ is not defined
class Basket:
    def __init__(self, items):
        self.items = items
    def __len__(self):
        return len(self.items)

print(bool(Basket([1, 2, 3])))
print(bool(Basket([])))
```

Output:
```
True
False
```

```python
# and/or return actual VALUES, not strict True/False
print(5 and 10)         # 10 -- returns last truthy operand
print(0 and 10)          # 0  -- returns first falsy operand
print("" or "default")    # 'default' -- common pattern for fallback values
```

Output:
```
10
0
default
```

### Common Mistakes

```python
# Mistake: assuming a string that "looks" false is falsy
user_input = "false"
if user_input:
    print("Truthy! This string is non-empty.")   # This runs — surprising to beginners
```

Output:
```
Truthy! This string is non-empty.
```

```python
# Fix: explicitly compare content, not just truthiness
if user_input.lower() == "false":
    print("User said false")
else:
    print("User said something else")
```

Output:
```
User said false
```

### Best Practices

> **Warning:** Never assume a string like `"False"`, `"0"`, or `"no"` is falsy — only the *empty string* `""` is falsy. Always compare content explicitly for text-based flags.

> **Tip:** Use `if collection:` instead of `if len(collection) > 0:` — it's more Pythonic and equally clear.

> **Tip:** Implement `__bool__` (or `__len__`) on custom classes when "emptiness" or "validity" is a meaningful concept for that object.

### Comparison: Falsy vs Truthy Quick Reference

| Value | `bool()` Result |
|---|---|
| `0`, `0.0`, `0j` | `False` |
| any nonzero number | `True` |
| `""` | `False` |
| `" "` (whitespace) | `True` |
| `[]`, `{}`, `()`, `set()` | `False` |
| `[0]`, `{0: 0}` | `True` (non-empty, contents irrelevant) |
| `None` | `False` |
| `float('nan')` | `True` |

### Key Takeaways

- `bool()` follows Python's truthiness rules: zero-like and empty values are falsy, everything else is truthy.
- A non-empty string is **always** truthy, regardless of its content.
- `and`/`or` return operand values, not strict booleans — useful for default-value patterns.
- Custom classes can define truthiness via `__bool__` or `__len__`.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 8. Arithmetic and Assignment Operators

### Definition

**Arithmetic operators** perform mathematical computations on numeric values. **Assignment operators** store a value into a variable, optionally combined with an arithmetic operation (compound/augmented assignment).

### Purpose / Why It Is Used

Arithmetic operators are the basis of all numeric computation. Assignment operators let you update a variable's value concisely, reducing repetition (e.g., `x += 1` instead of `x = x + 1`).

### Syntax

```python
a + b     a - b     a * b     a / b
a // b    a % b     a ** b

x = value
x += value    x -= value    x *= value
x /= value    x //= value   x %= value
x **= value
```

### Detailed Explanation

**Arithmetic operators:**

| Operator | Name | Example | Result |
|---|---|---|---|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `5 - 3` | `2` |
| `*` | Multiplication | `5 * 3` | `15` |
| `/` | True division | `5 / 2` | `2.5` |
| `//` | Floor division | `5 // 2` | `2` |
| `%` | Modulus | `5 % 2` | `1` |
| `**` | Exponentiation | `5 ** 2` | `25` |

**Assignment operators:**

| Operator | Equivalent To |
|---|---|
| `=` | `x = value` |
| `+=` | `x = x + value` |
| `-=` | `x = x - value` |
| `*=` | `x = x * value` |
| `/=` | `x = x / value` |
| `//=` | `x = x // value` |
| `%=` | `x = x % value` |
| `**=` | `x = x ** value` |

### Examples

```python
a, b = 7, 2
print(a + b, a - b, a * b, a / b, a // b, a % b, a ** b)
```

Output:
```
9 5 14 3.5 3 1 49
```

```python
x = 10
x += 5    # 15
x -= 3    # 12
x *= 2    # 24
x /= 4    # 6.0
print(x)
```

Output:
```
6.0
```

```python
# Walrus operator (assignment expression, Python 3.8+)
if (n := 10) > 5:
    print(f"n is {n}")
```

Output:
```
n is 10
```

### Real-World Use Cases

- Calculating totals, averages, discounts in e-commerce logic.
- Running counters in loops: `count += 1`.
- Pagination logic using `//` (floor division) and `%` (modulus) for page/remainder math.
- Compound interest / exponential growth calculations using `**`.

### Important Points / Rules

- `/` (true division) **always** returns a `float`, even for two integers that divide evenly.
- `//` (floor division) rounds **toward negative infinity**, not toward zero — this matters with negative numbers.
- `%` (modulus) result takes the **sign of the divisor**, not the dividend.
- `**` is right-associative: `2 ** 3 ** 2` evaluates as `2 ** (3 ** 2)`, not `(2 ** 3) ** 2`.
- Augmented assignment on **mutable** objects (like lists) can mutate in place, unlike a plain `x = x + y`.

### Common Mistakes

```python
# Mistake 1: Assuming floor division rounds toward zero
print(7 // 2)      # 3
print(-7 // 2)       # ⚠️ -4, NOT -3! Floors toward negative infinity
```

Output:
```
3
-4
```

```python
# Mistake 2: Assuming modulus always returns a non-negative result
print(7 % 3)         # 1
print(-7 % 3)          # ⚠️ 2, NOT -1! Result takes the sign of the divisor
```

Output:
```
1
2
```

```python
# Mistake 3: Division by zero
try:
    print(5 / 0)
except ZeroDivisionError as e:
    print("Error:", e)
```

Output:
```
Error: division by zero
```

```python
# Mistake 4: Assuming augmented assignment always behaves like reassignment
lst = [1, 2, 3]
lst2 = lst
lst += [4]           # in-place extend for mutable lists
print(lst, lst2)       # ⚠️ both changed, since += mutates the SAME list object
```

Output:
```
[1, 2, 3, 4] [1, 2, 3, 4]
```

### Best Practices

> **Tip:** Use `//` and `%` together (`divmod(a, b)`) when you need both quotient and remainder — it's cleaner and slightly faster than computing them separately.

> **Warning:** Be cautious with `+=` on lists shared across multiple variable names — it mutates in place and affects all references to that object.

> **Tip:** Wrap division operations in a `try`/`except ZeroDivisionError` block whenever the divisor could plausibly be zero (e.g., user input, computed averages).

### Comparison: `/` vs `//`

| Aspect | `/` (True Division) | `//` (Floor Division) |
|---|---|---|
| Return type | Always `float` | `int` if both operands are `int`, else `float` |
| Result for `7, 2` | `3.5` | `3` |
| Result for `-7, 2` | `-3.5` | `-4` (floors toward -∞) |
| Common use | Precise division | Integer division, pagination indices |

### Key Takeaways

- Python has seven arithmetic operators, including floor division (`//`) and exponentiation (`**`).
- `/` always returns `float`; `//` floors toward negative infinity; `%` takes the divisor's sign.
- Augmented assignment operators are shorthand, but can mutate objects in place for mutable types like lists.
- `**` is right-associative, unlike most other operators.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 9. Comparison and Logical Operators

### Definition

**Comparison operators** compare two values and produce a `bool` result. **Logical operators** (`and`, `or`, `not`) combine or invert boolean expressions to build more complex conditions.

### Purpose / Why It Is Used

These operators are the backbone of all decision-making logic — `if` statements, `while` loops, filtering data, and validating conditions all depend on them.

### Syntax

```python
a == b    a != b    a > b    a < b    a >= b    a <= b
a is b    a is not b
a in b    a not in b

a and b   a or b    not a
```

### Detailed Explanation

**Comparison operators:**

| Operator | Meaning |
|---|---|
| `==` | Equal to (value comparison) |
| `!=` | Not equal to |
| `>`, `<` | Greater / less than |
| `>=`, `<=` | Greater/less than or equal to |
| `is`, `is not` | Identity comparison (same object in memory) |
| `in`, `not in` | Membership test |

**Logical operators:**

| Operator | Behavior |
|---|---|
| `and` | Returns the first falsy operand, or the last operand if all are truthy |
| `or` | Returns the first truthy operand, or the last operand if all are falsy |
| `not` | Inverts truthiness, always returns strict `True`/`False` |

### Examples

```python
print(5 == 5, 5 != 3, 5 > 3, 5 < 3, 5 >= 5, 5 <= 4)
```

Output:
```
True True True False True False
```

```python
# Chained comparisons (Pythonic!)
x = 5
print(1 < x < 10)     # equivalent to (1 < x) and (x < 10)
```

Output:
```
True
```

```python
# is vs ==
a = [1, 2, 3]
b = [1, 2, 3]
c = a
print(a == b)    # True  -- same VALUE
print(a is b)     # False -- different OBJECTS
print(a is c)      # True  -- same object
```

Output:
```
True
False
True
```

```python
# Short-circuit evaluation
def side_effect():
    print("called!")
    return True

print(False and side_effect())   # side_effect() never runs
print(True or side_effect())      # side_effect() never runs
```

Output:
```
False
True
```

### Real-World Use Cases

- Validating login credentials: `if username == stored_user and password == stored_pass:`
- Filtering data: `[x for x in items if x > 0]`
- Checking membership in allowed values: `if role in ("admin", "editor"):`
- Guarding against `None` before attribute access: `if obj is not None and obj.value > 0:`

### Important Points / Rules

- Use `==` to compare **values**; use `is` to compare **object identity** (whether two names point to the exact same object in memory).
- `is` should be used for singleton comparisons like `None`, `True`, `False` — not for general value equality.
- Comparing different, incompatible types with `<`/`>` raises `TypeError` (e.g., `5 < "5"`).
- `and`/`or` use **short-circuit evaluation** — the right operand is not evaluated if the result is already determined.
- `and`/`or` return actual operand **values**, not necessarily strict booleans.

### Common Mistakes

```python
# Mistake 1: Using 'is' instead of '==' for value comparison
a = 1000
b = 1000
print(a is b)     # ⚠️ Often False -- large ints usually aren't cached/interned
print(a == b)      # ✅ True -- correct way to compare values
```

Output:
```
False
True
```

```python
# Mistake 2: Comparing incompatible types
try:
    print(5 < "5")
except TypeError as e:
    print("Error:", e)
```

Output:
```
Error: '<' not supported between instances of 'int' and 'str'
```

```python
# Mistake 3: Misjudging operator precedence with bitwise vs comparison
x = 5
print(x & 1 == 1)      # ⚠️ Evaluated as x & (1 == 1) due to precedence!
print((x & 1) == 1)      # ✅ Correct, explicit intent
```

Output:
```
1
True
```

### Best Practices

> **Tip:** Use `is` / `is not` only for identity checks — most notably `is None`, `is True`, `is False`. Use `==` for everything else.

> **Warning:** Bitwise operators (`&`, `|`, `^`) have **lower** precedence than comparison operators — always parenthesize when mixing them.

> **Tip:** Take advantage of short-circuit evaluation for safe guard conditions, e.g., `if obj is not None and obj.value > 0:` — the second check only runs if `obj` isn't `None`.

### Comparison: `==` vs `is`

| Aspect | `==` | `is` |
|---|---|---|
| Compares | Value/content | Object identity (memory address) |
| Use for | General equality checks | `None`, singleton checks |
| Can be overridden? | Yes (`__eq__`) | No |
| Example | `[1,2] == [1,2]` → `True` | `[1,2] is [1,2]` → `False` |

### Key Takeaways

- `==` compares values; `is` compares object identity — use each appropriately.
- Chained comparisons (`1 < x < 10`) are valid, readable Python.
- `and`/`or` short-circuit and return operand values, not strict booleans.
- Watch operator precedence when mixing bitwise and comparison operators — use parentheses.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 10. Associativity and Precedence of Operators

### Definition

**Precedence** determines which operator is evaluated first when an expression contains multiple different operators. **Associativity** determines the evaluation order when operators of the **same** precedence appear together — either left-to-right or right-to-left.

### Purpose / Why It Is Used

Understanding precedence and associativity is essential for writing expressions that evaluate the way you intend, and for reading/debugging complex expressions written by others — without this understanding, subtle bugs (like `-3 ** 2` evaluating to `-9`) are easy to miss.

### Syntax

There's no special syntax — precedence/associativity apply automatically. Parentheses `()` are used to override default evaluation order explicitly.

### Detailed Explanation

**Precedence table (highest to lowest):**

| Precedence | Operator(s) | Associativity |
|---|---|---|
| 1 (highest) | `()` grouping | — |
| 2 | `**` exponentiation | Right-to-left |
| 3 | `+x`, `-x`, `~x` (unary) | Right-to-left |
| 4 | `*`, `/`, `//`, `%` | Left-to-right |
| 5 | `+`, `-` (binary) | Left-to-right |
| 6 | `<<`, `>>` | Left-to-right |
| 7 | `&` | Left-to-right |
| 8 | `^` | Left-to-right |
| 9 | `\|` | Left-to-right |
| 10 | Comparisons (`==`, `!=`, `<`, `>`, `is`, `in`, ...) | Left-to-right (chained) |
| 11 | `not` | Right-to-left |
| 12 | `and` | Left-to-right |
| 13 (lowest) | `or` | Left-to-right |

### Examples

```python
print(2 + 3 * 4)          # * before +
print((2 + 3) * 4)          # parens override
```

Output:
```
14
20
```

```python
# ** is RIGHT-to-LEFT associative
print(2 ** 3 ** 2)        # 2 ** (3 ** 2) = 2 ** 9 = 512, NOT (2**3)**2 = 64
```

Output:
```
512
```

```python
# - and / are LEFT-to-RIGHT associative
print(10 - 3 - 2)           # (10-3)-2 = 5
print(20 / 4 / 2)             # (20/4)/2 = 2.5
```

Output:
```
5
2.5
```

```python
# Unary minus has LOWER precedence than **
print(-2 ** 2)          # -(2**2) = -4
print((-2) ** 2)          # (−2)**2 = 4
```

Output:
```
-4
4
```

```python
# Logical operator precedence: not > and > or
print(True or True and False)   # and evaluates first: True and False = False; then True or False = True
print(not False and True)         # not evaluates first: not False = True; then True and True = True
```

Output:
```
True
True
```

### Real-World Use Cases

- Writing correct mathematical/financial formulas without unnecessary parentheses.
- Debugging unexpected results in conditional logic that mixes `and`/`or`/`not`.
- Avoiding bugs when mixing bitwise operators with comparisons (common in flag-based logic).
- Writing readable, unambiguous expressions in data validation and filtering code.

### Important Points / Rules

- `**` binds tighter than unary minus: `-3 ** 2` is `-9`, not `9`.
- `**` is the only common arithmetic operator that is right-associative; most others are left-associative.
- Bitwise operators (`&`, `^`, `|`) have **lower** precedence than comparison operators — a frequent source of bugs when checking flags.
- `not` has **higher** precedence than `and`, which has **higher** precedence than `or`.
- When in doubt, **use parentheses** — they cost nothing and eliminate ambiguity for future readers (including yourself).

### Common Mistakes

```python
# Mistake 1: Assuming exponentiation is left-associative
print(2 ** 3 ** 2)     # ⚠️ 512, not 64 -- many beginners expect (2**3)**2

# Mistake 2: Forgetting unary minus binds looser than **
print(-4 ** 0.5)          # ⚠️ -2.0, computed as -(4**0.5), NOT sqrt(-4)
```

Output:
```
512
-2.0
```

```python
# Mistake 3: Mixing bitwise and comparison operators without parentheses
x = 5
print(x & 1 == 1)        # ⚠️ Evaluated as x & (1 == 1) → x & True → x & 1 = 1
print((x & 1) == 1)         # ✅ True -- correct, explicit
```

Output:
```
1
True
```

```python
# Mistake 4: Assuming 'and'/'or' have equal precedence
print(True or False and False)     # and binds tighter -- evaluated as True or (False and False) = True
```

Output:
```
True
```

### Best Practices

> **Tip:** When combining more than two different operator types in one expression, add parentheses even if not strictly required — it drastically improves readability.

> **Warning:** Always parenthesize when mixing bitwise operators (`&`, `|`, `^`) with comparisons — their low precedence is a very common bug source.

> **Tip:** Memorize the "PEMDAS-like" order for Python: Parentheses → Exponent → Unary +/- → Multiplication/Division/Floor-Div/Modulus → Addition/Subtraction → Comparisons → not → and → or.

### Comparison: Left vs Right Associativity

| Associativity | Applies To | Example | Evaluation Order |
|---|---|---|---|
| Left-to-right | `+`, `-`, `*`, `/`, `and`, `or` | `10 - 3 - 2` | `(10-3)-2` |
| Right-to-left | `**`, unary `-` | `2 ** 3 ** 2` | `2**(3**2)` |

### Key Takeaways

- Precedence decides which operator runs first among different operators; associativity decides order among same-precedence operators.
- `**` is right-associative and binds tighter than unary minus — both are common surprise sources.
- Bitwise operators have lower precedence than comparisons — always parenthesize when mixing them.
- Parentheses are the simplest, safest way to guarantee intended evaluation order.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 11. Printing to the Console — the print() Function

### Definition

`print()` is a built-in function that writes text (or the string representation of objects) to standard output — typically the console — followed by a newline character by default.

### Purpose / Why It Is Used

`print()` is the most basic and widely used way to display information to a user or developer: debugging values, showing results, and building simple text-based interfaces.

### Syntax

```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

| Parameter | Meaning | Default |
|---|---|---|
| `*objects` | One or more values to print | — |
| `sep` | String inserted between multiple objects | `' '` (space) |
| `end` | String appended after the last object | `'\n'` (newline) |
| `file` | Output stream/destination | `sys.stdout` (console) |
| `flush` | Force immediate flush of the output buffer | `False` |

### Detailed Explanation

```python
print("Hello, World!")
```

Output:
```
Hello, World!
```

```python
# Multiple arguments, joined by sep (default: space)
print("Hello", "World", "!")
```

Output:
```
Hello World !
```

```python
# Custom separator
print("2024", "01", "15", sep="-")
```

Output:
```
2024-01-15
```

```python
# Custom end (default is newline)
print("Hello", end=" ")
print("World")
```

Output:
```
Hello World
```

```python
# f-strings inside print()
name = "Alice"
pi = 3.14159265
print(f"Hello, {name}! Pi is {pi:.2f}")
```

Output:
```
Hello, Alice! Pi is 3.14
```

```python
# Printing to a file instead of the console
with open("output.txt", "w") as f:
    print("Written to file", file=f)
```

### Real-World Use Cases

- Debugging: quickly inspecting variable values during development.
- Building simple CLI (command-line interface) tools and scripts.
- Logging progress in scripts, loops, or long-running processes.
- Writing formatted output to a log file using `file=`.

### Important Points / Rules

- `print()` **always returns `None`** — never use its return value.
- `sep` applies **only between** arguments, never before the first or after the last.
- `print()` calls the object's `__str__` method (falling back to `__repr__`) to determine what to display.
- `flush=True` forces immediate output — useful in loops with delays, or when piping output to another process.

### Examples: Edge Cases

```python
# print() with no arguments prints a blank line
print()
```

```python
# end='' avoids the newline, useful for progress indicators
for i in range(3):
    print(i, end=" ")
print()
```

Output:
```
0 1 2 
```

```python
# Custom __str__ controls how an object prints
class Point:
    def __init__(self, x, y):
        self.x, self.y = x, y
    def __str__(self):
        return f"Point({self.x}, {self.y})"

print(Point(1, 2))
```

Output:
```
Point(1, 2)
```

### Common Mistakes

```python
# Mistake 1: Trying to use print()'s return value
result = print("hello")
print(result)     # ⚠️ prints "hello" then "None" -- print() always returns None
```

Output:
```
hello
None
```

```python
# Mistake 2: Forgetting str() conversion isn't needed for print() (unlike concatenation)
age = 25
print("Age:", age)     # ✅ works fine -- print() auto-converts each argument
# print("Age: " + age) # ❌ would raise TypeError if you used + instead
```

Output:
```
Age: 25
```

### Best Practices

> **Tip:** Use `sep` and `end` instead of manually building strings with `+` when printing multiple related values.

> **Tip:** Use `flush=True` in loops with `time.sleep()` calls to ensure output appears in real time rather than being buffered.

> **Warning:** Don't rely on `print()`'s return value in expressions — it's always `None`.

### Comparison: print() vs f-string vs .format()

| Approach | Example | Best For |
|---|---|---|
| `print()` with commas | `print("Age:", age)` | Quick debugging, simple output |
| f-string inside `print()` | `print(f"Age: {age}")` | Formatted, readable output (recommended) |
| `.format()` | `print("Age: {}".format(age))` | Legacy codebases, dynamic templates |

### Key Takeaways

- `print()` writes to standard output, joining multiple arguments with `sep` and ending with `end` (default: newline).
- It always returns `None` — never chain or capture its result.
- Combine with f-strings for clean, readable formatted output.
- Use `file=` to redirect output to a file, and `flush=True` for real-time output in loops.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 12. Taking Input from the User — the input() Function

### Definition

`input()` is a built-in function that reads a single line of text typed by the user from standard input (the keyboard), pauses program execution until Enter is pressed, and returns the text as a **string**.

### Purpose / Why It Is Used

`input()` is the primary way console-based Python programs interact with a user — collecting names, numbers, choices, or any other text data needed to drive program logic.

### Syntax

```python
input(prompt='')
```

| Parameter | Meaning |
|---|---|
| `prompt` | Optional text displayed before waiting for input |

### Detailed Explanation

```python
name = input("Enter your name: ")
print(f"Hello, {name}!")
```

Output (given input `Saurabh`):
```
Enter your name: Saurabh
Hello, Saurabh!
```

```python
# input() ALWAYS returns a string -- convert manually for numbers
age = int(input("Enter your age: "))
print(f"Next year you'll be {age + 1}")
```

Output (given input `25`):
```
Enter your age: 25
Next year you'll be 26
```

```python
# Reading multiple values on one line
a, b = map(int, input("Enter two numbers: ").split())
print(a + b)
```

Output (given input `3 7`):
```
Enter two numbers: 3 7
10
```

```python
# Reading a list of numbers
values = list(map(int, input("Enter numbers separated by space: ").split()))
print(values)
```

Output (given input `1 2 3 4`):
```
Enter numbers separated by space: 1 2 3 4
[1, 2, 3, 4]
```

### Real-World Use Cases

- Command-line tools that collect configuration or arguments interactively.
- Simple quizzes, calculators, and games run in the terminal.
- Prompting for confirmation before a destructive action (`Continue? (y/n)`).
- Collecting structured data (comma-separated values) for quick scripts.

### Important Points / Rules

- `input()` **always returns a `str`**, regardless of what the user types — numeric conversion is always manual.
- If the user presses Enter without typing anything, `input()` returns an **empty string** (`''`), not `None`.
- `input()` raises `EOFError` if the input stream is closed unexpectedly (e.g., piped input runs out).
- Leading/trailing whitespace in user input is preserved unless explicitly stripped with `.strip()`.
- **Never use `eval()`** on raw user input — it can execute arbitrary code and is a serious security risk.

### Common Mistakes

```python
# Mistake 1: Forgetting input() returns a string
x = input("Enter a number: ")     # user types: 42
# print(x + 1)     # ❌ TypeError: can only concatenate str (not "int") to str
print(int(x) + 1)    # ✅ correct
```

Output (given input `42`):
```
Enter a number: 42
43
```

```python
# Mistake 2: Not handling invalid numeric input
try:
    num = int(input("Enter a number: "))     # user types "abc"
except ValueError:
    print("Invalid input! Please enter digits only.")
```

Output (given input `abc`):
```
Enter a number: abc
Invalid input! Please enter digits only.
```

```python
# Mistake 3: Assuming split() always returns the expected count
try:
    a, b = input("Enter two numbers: ").split()   # user enters "1 2 3"
except ValueError as e:
    print("Error:", e)
```

Output (given input `1 2 3`):
```
Enter two numbers: 1 2 3
Error: too many values to unpack (expected 2)
```

```python
# Mistake 4 (SECURITY): using eval() on user input
# unsafe = eval(input("Enter expression: "))   # ❌ DANGEROUS -- can run arbitrary code

# Safer alternative for literal values:
import ast
safe_value = ast.literal_eval("42")
print(safe_value)
```

Output:
```
42
```

### Best Practices

> **Tip:** Always validate and convert `input()` results inside a `try`/`except` block when expecting numeric data.

> **Tip:** Use `.strip()` on user input before comparing or validating it, to avoid whitespace-related bugs.

> **Warning:** Never pass raw `input()` directly to `eval()` — use `int()`, `float()`, or `ast.literal_eval()` instead for safe parsing.

### Examples: Robust Input Validation Loop

```python
while True:
    user_input = input("Enter a positive number: ")
    if user_input.isdigit():
        num = int(user_input)
        break
    else:
        print("Invalid input, try again.")
print(f"You entered: {num}")
```

Output (given inputs `abc`, then `15`):
```
Enter a positive number: abc
Invalid input, try again.
Enter a positive number: 15
You entered: 15
```

### Comparison: input() vs sys.stdin vs argparse

| Method | Use Case | Blocking? |
|---|---|---|
| `input()` | Simple, single-line interactive prompts | Yes, waits for Enter |
| `sys.stdin.read()` | Reading multi-line or piped input | Yes, until EOF |
| `argparse` | Command-line arguments passed at launch | No (non-interactive) |

### Key Takeaways

- `input()` always returns a string and pauses execution until the user presses Enter.
- Convert the result explicitly with `int()`/`float()` when numeric data is needed, and handle `ValueError`.
- Empty input returns `''`, not `None`; unexpected stream closure raises `EOFError`.
- Never use `eval()` on user input — prefer safe conversion functions or `ast.literal_eval()`.

[⬆ Back to Table of Contents](#table-of-contents)

---
## 13. Overall Summary

This guide walked through the essential building blocks every Python program is made of:

- **Literals** are the raw values you write directly in code — numeric, string, boolean, `None`, and collection literals.
- **Variables** are names bound to objects in memory; Python is dynamically typed, so a name can be rebound to any type at any time.
- **Keywords** are reserved words (`if`, `def`, `class`, `and`, etc.) that Python's grammar depends on and that cannot be used as identifiers.
- **Primitive datatypes** (`int`, `float`, `complex`, `str`, `bool`, `NoneType`) are the fundamental scalar building blocks for all data.
- **String operations** cover creating, slicing, searching, and formatting text — one of the most frequently used skills in any Python program.
- **Type conversion (`int`, `float`, `str`)** moves data safely between numeric and text representations, with truncation and parsing rules to watch for.
- **Type conversion (`bool`)** follows truthiness rules — every value is inherently truthy or falsy, which powers conditionals throughout Python.
- **Arithmetic and assignment operators** perform and store calculations, with important nuances around floor division, modulus sign, and mutability.
- **Comparison and logical operators** drive all decision-making logic, distinguishing value equality (`==`) from identity (`is`).
- **Precedence and associativity** determine evaluation order in complex expressions — critical for both writing correct code and reading others' code accurately.
- **`print()`** is the primary way to display output to the console, with fine control via `sep`, `end`, and `file`.
- **`input()`** is the primary way to collect data from a user, always returning a string that must be explicitly converted as needed.

Together, these twelve topics form the complete foundation for everything else in Python — control flow, functions, object-oriented programming, and beyond all build directly on these fundamentals.

[⬆ Back to Table of Contents](#table-of-contents)

---

## 14. Quick Revision / Cheat Sheet

### Datatypes at a Glance

| Type | Example | Mutable? | `bool()` False When |
|---|---|---|---|
| `int` | `42` | No | `0` |
| `float` | `3.14` | No | `0.0` |
| `complex` | `3+4j` | No | `0j` |
| `str` | `"hi"` | No | `""` |
| `bool` | `True` | No | `False` |
| `list` | `[1,2]` | Yes | `[]` |
| `tuple` | `(1,2)` | No | `()` |
| `dict` | `{"a":1}` | Yes | `{}` |
| `set` | `{1,2}` | Yes | `set()` |
| `NoneType` | `None` | No | always `False` |

### Operator Quick Reference

| Category | Operators |
|---|---|
| Arithmetic | `+  -  *  /  //  %  **` |
| Assignment | `=  +=  -=  *=  /=  //=  %=  **=` |
| Comparison | `==  !=  >  <  >=  <=` |
| Identity | `is  is not` |
| Membership | `in  not in` |
| Logical | `and  or  not` |

### Precedence Cheat Sheet (High → Low)

```
()                              # grouping
**                               # exponent (right-to-left)
+x  -x  ~x                        # unary
*  /  //  %                        # multiplicative
+  -                                # additive
<<  >>                               # bitwise shift
&                                     # bitwise AND
^                                      # bitwise XOR
|                                       # bitwise OR
==  !=  <  >  <=  >=  is  in            # comparisons
not                                       # logical NOT
and                                        # logical AND
or                                          # logical OR (lowest)
```

### Type Conversion Quick Reference

| From → To | Function | Gotcha |
|---|---|---|
| str → int | `int("42")` | Fails on decimals; use `int(float(x))` |
| float → int | `int(3.9)` | Truncates, doesn't round |
| str → float | `float("3.14")` | Supports `"inf"`, `"nan"` |
| any → str | `str(x)` | Rarely fails |
| any → bool | `bool(x)` | Only falsy: `0`, `""`, `[]`, `{}`, `()`, `None`, `set()` |

### String Methods Quick Reference

| Method | Purpose |
|---|---|
| `.upper()` / `.lower()` | Case conversion |
| `.strip()` | Remove leading/trailing whitespace |
| `.split(sep)` | String → list |
| `.join(list)` | List → string |
| `.replace(old,new)` | Substitution |
| `.find(sub)` | Index or `-1` |
| `.startswith()` / `.endswith()` | Prefix/suffix check |

### print() / input() Quick Reference

```python
print(a, b, sep=", ", end="\n")     # custom separator and ending
name = input("Prompt: ")               # always returns str
age = int(input("Age: "))                # convert immediately when needed
```

[⬆ Back to Table of Contents](#table-of-contents)

---

## 15. Common Interview Questions

**Q1. What is the difference between `is` and `==`?**
`==` compares the *values* of two objects, while `is` compares their *identity* — whether they are the exact same object in memory. Two equal-valued lists are usually `==` but not `is`.

**Q2. Why does `0.1 + 0.2 != 0.3` in Python?**
Floats are stored in IEEE 754 binary format, which cannot represent most decimal fractions exactly. Small rounding errors accumulate, so direct equality checks on floats are unreliable — use `math.isclose()` instead.

**Q3. Is `bool` a separate type from `int` in Python?**
No — `bool` is technically a **subclass** of `int`. `True` equals `1` and `False` equals `0`, and both participate in arithmetic (`True + True == 2`).

**Q4. What does `input()` return, and what's a common mistake with it?**
`input()` always returns a `str`, even if the user types a number. A common mistake is trying to use the result directly in arithmetic without converting it via `int()` or `float()` first, causing a `TypeError`.

**Q5. What's the difference between `/` and `//` in Python 3?**
`/` is true division and always returns a `float`. `//` is floor division — it returns the largest integer less than or equal to the mathematical result, flooring toward negative infinity (not toward zero) for negative operands.

**Q6. Why is `-3 ** 2` equal to `-9` and not `9`?**
Because `**` has higher precedence than unary minus. The expression is evaluated as `-(3 ** 2)`, i.e., `-(9)`, not `(-3) ** 2`.

**Q7. What values are considered "falsy" in Python?**
`0`, `0.0`, `0j`, `""`, `[]`, `()`, `{}`, `set()`, and `None`. Every other value, including non-empty strings like `"False"`, is truthy.

**Q8. What happens if you use a Python keyword as a variable name?**
Python raises a `SyntaxError` immediately, since keywords are reserved and cannot be reassigned or used as identifiers.

**Q9. How would you safely convert user input to an integer, handling invalid input?**
Wrap the conversion in a `try`/`except ValueError` block:
```python
try:
    num = int(input("Enter a number: "))
except ValueError:
    print("Invalid input")
```

**Q10. What is the difference between mutable and immutable types, and why does it matter for variable assignment?**
Mutable types (list, dict, set) can be changed in place; immutable types (int, str, tuple) cannot. When you assign `b = a` for a mutable object, both names reference the *same* object, so modifying one affects the other. For immutable types, reassignment always creates a new object, leaving the original untouched.

**Q11. Why does `and`/`or` not always return `True`/`False`?**
Because Python's `and`/`or` are *value-returning* short-circuit operators — they return whichever operand determined the result, not a coerced boolean. `5 or 10` returns `5`, not `True`.

**Q12. What's the difference between `str.split()` with no arguments and `str.split(" ")`?**
`.split()` with no arguments splits on any run of whitespace and discards empty strings. `.split(" ")` splits strictly on single-space characters and keeps empty strings that result from consecutive spaces.

[⬆ Back to Table of Contents](#table-of-contents)

---

## 16. Practice Exercises

Try to solve each of these before checking your understanding against the corresponding topic section above.

1. **Literals:** Write a single expression using binary, octal, and hexadecimal literals that all evaluate to the decimal number `255`.
2. **Variables:** Given `a = [1, 2, 3]` and `b = a`, explain (without running it) what happens to `a` if you run `b.append(4)`. Then verify by running the code.
3. **Keywords:** Write a snippet that intentionally tries to use `class` as a variable name, and explain the error Python gives.
4. **Primitive Datatypes:** Predict the output of `print(0.1 + 0.2 == 0.3)` and explain why, then fix the comparison using `math.isclose()`.
5. **Strings:** Given `s = "  Python Programming  "`, write code to: (a) strip whitespace, (b) convert to lowercase, (c) replace spaces with underscores — all in one chained expression.
6. **Type Conversion (numeric):** Write a function that safely converts a string to a float, returning `None` if the conversion fails, using `try`/`except`.
7. **Type Conversion (bool):** Predict and then verify the output of `bool("0")`, `bool(0)`, `bool("")`, and `bool([0])`.
8. **Arithmetic/Assignment:** Without running it, predict the output of `-7 // 2` and `-7 % 2`, then verify.
9. **Comparison/Logical:** Write a chained comparison that checks whether a variable `score` is between `0` and `100` inclusive, without using `and` explicitly.
10. **Precedence:** Predict the output of `2 + 3 * 2 ** 2 - 1` step by step, then verify with Python.
11. **print():** Write a `print()` statement that outputs `A-B-C` on one line using the `sep` parameter, without manually inserting hyphens into the string.
12. **input():** Write a program that prompts the user for three numbers on a single line (space-separated), converts them to integers, and prints their sum and average.

### Sample Solution (Exercise 12)

```python
nums = list(map(int, input("Enter three numbers separated by spaces: ").split()))
total = sum(nums)
average = total / len(nums)
print(f"Sum: {total}, Average: {average:.2f}")
```

Output (given input `4 8 15`):
```
Enter three numbers separated by spaces: 4 8 15
Sum: 27, Average: 9.00
```

[⬆ Back to Table of Contents](#table-of-contents)
