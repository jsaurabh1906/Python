# Python Control Statements: Decision-Making with `if`, `if-else`, `if-elif-else`, Nested `if`, and the Ternary Operator

## Introduction

By default, Python runs a program **top to bottom, one statement at a time**. Real programs need to make decisions: grant access only if the password is correct, charge a delivery fee only if the order is small, print "Pass" or "Fail" depending on marks.

**Control statements** let a program choose which code to run based on conditions. This guide covers the **conditional (decision-making) statements** in Python:

1. The `if` block
2. The `if-else` block
3. The `if-elif-else` ladder
4. Nested `if` statements
5. The ternary (conditional) operator

Each topic moves from simple to advanced, with definitions, syntax, examples with output, real-world uses, common mistakes, and best practices.

---

## Table of Contents

1. [Control Statements Overview](#1-control-statements-overview)
2. [Building Blocks of Conditions](#2-building-blocks-of-conditions)
   - [2.1 Comparison Operators](#21-comparison-operators)
   - [2.2 Logical Operators](#22-logical-operators)
   - [2.3 Truthy and Falsy Values](#23-truthy-and-falsy-values)
   - [2.4 Indentation Rules](#24-indentation-rules)
3. [The `if` Block](#3-the-if-block)
4. [The `if-else` Block](#4-the-if-else-block)
5. [The `if-elif-else` Ladder](#5-the-if-elif-else-ladder)
6. [Nested `if` Statements](#6-nested-if-statements)
7. [The Ternary Operator](#7-the-ternary-operator)
8. [How the Topics Connect](#8-how-the-topics-connect)
9. [Overall Summary](#9-overall-summary)
10. [Quick Revision / Cheat Sheet](#10-quick-revision--cheat-sheet)
11. [Common Interview Questions](#11-common-interview-questions)
12. [Practice Questions / Exercises](#12-practice-questions--exercises)

---

## 1. Control Statements Overview

### 1.1 Definition

A **control statement** is a statement that changes the normal top-to-bottom flow of execution. Python has three categories:

| Category | Purpose | Examples |
|---|---|---|
| **Conditional (selection)** | Choose which block runs based on a condition | `if`, `if-else`, `if-elif-else`, ternary |
| **Iterative (looping)** | Repeat a block multiple times | `for`, `while` |
| **Transfer (jump)** | Alter loop or program flow | `break`, `continue`, `pass` |

This document covers only the **conditional** category.

### 1.2 Why Are They Needed?

Without conditions, a program would do exactly the same thing every time. Conditions make programs **dynamic** and **responsive to data**.

### 1.3 Basic Flow

```
        ┌───────────┐
        │ Condition │
        └─────┬─────┘
       True   │   False
     ┌────────┴────────┐
     ▼                 ▼
 Run block A       Run block B / skip
```

### Key Takeaways

- Control statements decide **which code runs**.
- This guide covers the *conditional* type.
- Every conditional statement relies on a condition that evaluates to `True` or `False`.

---

## 2. Building Blocks of Conditions

Before writing decisions, you need to understand what goes inside the condition.

### 2.1 Comparison Operators

These compare two values and return a Boolean (`True` or `False`).

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `3 > 5` | `False` |
| `<` | Less than | `3 < 5` | `True` |
| `>=` | Greater than or equal to | `5 >= 5` | `True` |
| `<=` | Less than or equal to | `4 <= 3` | `False` |

Python also supports **chained comparisons**:

```python
age = 25
print(18 <= age <= 60)
```

**Output:**

```
True
```

> **Note:** `18 <= age <= 60` is equivalent to `18 <= age and age <= 60`, but shorter and more readable.

### 2.2 Logical Operators

Logical operators combine multiple conditions.

| Operator | Meaning | Returns `True` when |
|---|---|---|
| `and` | Logical AND | **Both** conditions are true |
| `or` | Logical OR | **At least one** condition is true |
| `not` | Logical NOT | The condition is false (it reverses the result) |

**Truth table:**

| A | B | `A and B` | `A or B` | `not A` |
|---|---|---|---|---|
| True | True | True | True | False |
| True | False | False | True | False |
| False | True | False | True | True |
| False | False | False | False | True |

```python
age = 25
has_id = True
print(age >= 18 and has_id)
print(age < 18 or has_id)
print(not has_id)
```

**Output:**

```
True
True
False
```

> **Note:** `and` and `or` use **short-circuit evaluation**. In `A and B`, if `A` is `False`, Python does not evaluate `B`. In `A or B`, if `A` is `True`, Python does not evaluate `B`. This is useful for avoiding errors, such as `if b != 0 and a / b > 2:`.

### 2.3 Truthy and Falsy Values

Python's `if` does not require a strict `True`/`False`. Any object can be tested, and Python treats it as either **truthy** or **falsy**.

| Falsy values | Truthy values |
|---|---|
| `False` | `True` |
| `None` | Any non-zero number (`1`, `-5`, `3.14`) |
| `0`, `0.0`, `0j` | Any non-empty string (`"hello"`, `" "`, `"0"`, `"False"`) |
| `""` (empty string) | Any non-empty list, tuple, set, dict |
| `[]`, `()`, `{}`, `set()` | Most other objects |

```python
name = ""
if name:
    print("Name provided")
else:
    print("Name is empty")
```

**Output:**

```
Name is empty
```

> **Warning:** The string `"0"` and the string `"False"` are **truthy** because they are non-empty strings.

### 2.4 Indentation Rules

Python uses **indentation** (leading whitespace) instead of braces `{}` to define blocks.

- Use **4 spaces** per level (the PEP 8 standard).
- All statements in the same block must have the **same indentation**.
- Do not mix tabs and spaces.

```python
if True:
    print("Inside block")     # indented: part of the if block
print("Outside block")        # not indented: runs regardless
```

**Output:**

```
Inside block
Outside block
```

### Key Takeaways

- Conditions use comparison operators (`==`, `!=`, `>`, `<`, `>=`, `<=`) and logical operators (`and`, `or`, `not`).
- Any value can be tested for truthiness. Empty or zero-like values are falsy.
- Indentation defines the block. It is syntax, not style.

---

## 3. The `if` Block

### 3.1 Definition

The **`if` statement** executes a block of code **only when its condition evaluates to `True`**. If the condition is `False`, the block is skipped.

### 3.2 Purpose / Why It Is Used

- To run code **conditionally**.
- To perform an action only in special cases (validation, alerts, discounts, etc.).
- It is the foundation of all other conditional statements.

### 3.3 Syntax

```python
if condition:
    # statement(s) executed when condition is True
```

| Part | Description |
|---|---|
| `if` | Keyword that starts the statement |
| `condition` | Any expression that evaluates to a truthy or falsy value |
| `:` | Colon (mandatory) marking the start of the block |
| Indented block | Code that runs only if the condition is true |

### 3.4 Flow of Execution

1. Python evaluates the condition.
2. If `True`, the indented block runs, then execution continues after the block.
3. If `False`, the indented block is skipped, and execution continues after the block.

### 3.5 Examples

#### Example 1: Basic usage

```python
age = 20

if age >= 18:
    print("You are eligible to vote.")

print("Program finished.")
```

**Output:**

```
You are eligible to vote.
Program finished.
```

**Explanation:** `age >= 18` is `True`, so the message prints. The last `print` is outside the block and always runs.

#### Example 2: Condition is False

```python
age = 15

if age >= 18:
    print("You are eligible to vote.")

print("Program finished.")
```

**Output:**

```
Program finished.
```

**Explanation:** The condition is `False`, so the block is skipped. Nothing is printed for it.

#### Example 3: Multiple statements in one block

```python
temperature = 38

if temperature > 37:
    print("High temperature detected!")
    print("Please consult a doctor.")
    print("Stay hydrated.")
```

**Output:**

```
High temperature detected!
Please consult a doctor.
Stay hydrated.
```

**Explanation:** All three indented lines belong to the same block, so they run together.

#### Example 4: User input

```python
number = int(input("Enter a number: "))

if number > 0:
    print("The number is positive.")
```

**Sample run 1:**

```
Enter a number: 7
The number is positive.
```

**Sample run 2:**

```
Enter a number: -3
```

*(No output, because the condition is false.)*

> **Note:** `input()` always returns a **string**. Convert it with `int()` or `float()` before comparing with numbers.

#### Example 5: Different data types

```python
# String comparison
city = "Pune"
if city == "Pune":
    print("Welcome to Pune!")

# Boolean value
is_logged_in = True
if is_logged_in:
    print("Access granted.")

# List (truthiness)
items = ["apple", "banana"]
if items:
    print(f"Cart has {len(items)} item(s).")
```

**Output:**

```
Welcome to Pune!
Access granted.
Cart has 2 item(s).
```

#### Example 6: Combining conditions

```python
age = 30
income = 50000

if age >= 21 and income >= 30000:
    print("Loan pre-approved.")
```

**Output:**

```
Loan pre-approved.
```

#### Example 7: Edge cases

```python
marks = 40

if marks >= 40:
    print("Boundary value 40 counts as pass.")

value = None
if value:
    print("This will NOT print (None is falsy).")

zero = 0
if zero:
    print("This will NOT print (0 is falsy).")
```

**Output:**

```
Boundary value 40 counts as pass.
```

**Explanation:** Always test the boundary values (`>=` vs `>`). `None` and `0` are falsy.

#### Example 8: Single-line `if`

```python
x = 10
if x > 5: print("x is greater than 5")
```

**Output:**

```
x is greater than 5
```

> **Tip:** This is valid but discouraged for anything beyond trivial cases. A multi-line block is more readable and easier to extend.

#### Example 9: Invalid input handling

```python
user_input = input("Enter your age: ")

if user_input.isdigit():
    age = int(user_input)
    if age >= 18:
        print("Adult")
```

**Sample run:**

```
Enter your age: abc
```

*(No output. `isdigit()` returned `False`, so the block never ran and no crash occurred.)*

> **Note:** `isdigit()` only accepts non-negative whole numbers. For negative or decimal input, use `try/except` with `int()` or `float()`.

### 3.6 Real-World Use Cases

| Scenario | Condition |
|---|---|
| Apply a discount | `if cart_total > 1000:` |
| Show a low battery warning | `if battery < 20:` |
| Validate a form field | `if not email:` |
| Send an alert | `if temperature > threshold:` |
| Check a file exists before reading | `if os.path.exists(path):` |

### 3.7 Important Points / Rules

- The condition must be followed by a **colon `:`**.
- The block must be **indented**, and it cannot be empty (use `pass` as a placeholder).
- Parentheses around the condition are **optional**: `if (x > 5):` works, but `if x > 5:` is preferred.
- Use `==` to compare and `=` to assign.
- Code after the block (same indentation as `if`) runs regardless.

### 3.8 Common Mistakes

| Mistake | Wrong code | Correct code |
|---|---|---|
| Using `=` instead of `==` | `if x = 5:` (SyntaxError) | `if x == 5:` |
| Missing colon | `if x > 5` (SyntaxError) | `if x > 5:` |
| Missing indentation | `if x > 5:` followed by an unindented `print(...)` (IndentationError) | Indent the body |
| Comparing string input to a number | `if input() > 5:` (TypeError) | `if int(input()) > 5:` |
| Redundant Boolean comparison | `if is_valid == True:` | `if is_valid:` |
| Misusing `or` | `if x == 1 or 2:` (always truthy) | `if x == 1 or x == 2:` or `if x in (1, 2):` |

> **Warning:** `if x == 1 or 2:` is parsed as `if (x == 1) or (2):`. Since `2` is always truthy, the whole condition is **always true**, whatever `x` is.

### 3.9 Best Practices

- Keep conditions **simple and readable**. Extract complex ones into named variables:

  ```python
  is_eligible = age >= 18 and has_id and not is_banned
  if is_eligible:
      print("Allowed")
  ```

- Use `if not x:` for emptiness or `None` checks. Use `if x is None:` when you must distinguish `None` from `0` or `""`.
- Use `in` for membership checks: `if day in ("Sat", "Sun"):`.
- Use `is` / `is not` for `None`, not `==`.

### Key Takeaways

- `if` runs a block **only when the condition is true**; otherwise it does nothing.
- A colon and consistent indentation are mandatory.
- Any value can be a condition, so learn the falsy values.
- Watch for `=` vs `==` and for incorrectly written `or` conditions.

---

## 4. The `if-else` Block

### 4.1 Definition

The **`if-else` statement** provides **two paths**: one block runs if the condition is `True`, and a different block runs if it is `False`. **Exactly one** of the two blocks always runs.

### 4.2 Purpose / Why It Is Used

- When you need to handle **both outcomes** of a yes/no decision.
- Examples: pass/fail, even/odd, login success/failure, adult/minor.

### 4.3 Syntax

```python
if condition:
    # runs when condition is True
else:
    # runs when condition is False
```

| Part | Description |
|---|---|
| `else` | Keyword with **no condition** of its own |
| `:` | Colon after `else` is mandatory |
| Alignment | `else` must line up with its matching `if` |

### 4.4 Flow of Execution

1. Evaluate the condition.
2. `True` → run the `if` block and **skip** `else`.
3. `False` → **skip** the `if` block and run `else`.

### 4.5 Examples

#### Example 1: Basic usage

```python
age = 16

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

**Output:**

```
Minor
```

#### Example 2: Even or odd (user input)

```python
number = int(input("Enter a number: "))

if number % 2 == 0:
    print(f"{number} is even.")
else:
    print(f"{number} is odd.")
```

**Sample runs:**

```
Enter a number: 10
10 is even.
```

```
Enter a number: 7
7 is odd.
```

```
Enter a number: 0
0 is even.
```

```
Enter a number: -3
-3 is odd.
```

**Explanation:** `%` gives the remainder. An even number leaves remainder `0` when divided by 2. In Python, `-3 % 2` is `1`, so negative odd numbers work correctly. Zero counts as even.

#### Example 3: Password check (strings)

```python
correct_password = "python123"
entered = "Python123"

if entered == correct_password:
    print("Login successful.")
else:
    print("Incorrect password.")
```

**Output:**

```
Incorrect password.
```

**Explanation:** String comparison is **case-sensitive**, so `"Python123"` is not equal to `"python123"`.

#### Example 4: Case-insensitive comparison

```python
answer = input("Do you want to continue? (yes/no): ")

if answer.strip().lower() == "yes":
    print("Continuing...")
else:
    print("Stopping.")
```

**Sample run:**

```
Do you want to continue? (yes/no):   YES 
Continuing...
```

> **Tip:** `.strip()` removes extra spaces and `.lower()` normalizes case. Together they make user-input comparisons more forgiving.

#### Example 5: Multiple values and conditions

```python
username = "admin"
password = "1234"

if username == "admin" and password == "1234":
    print("Welcome, Admin!")
else:
    print("Invalid credentials.")
```

**Output:**

```
Welcome, Admin!
```

#### Example 6: Leap year

```python
year = 2024

if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
    print(f"{year} is a leap year.")
else:
    print(f"{year} is not a leap year.")
```

**Output:**

```
2024 is a leap year.
```

**Explanation:** A year is a leap year if it is divisible by 4 but not by 100, **or** divisible by 400. Edge cases: `1900` → not leap, `2000` → leap.

#### Example 7: Invalid input with `try/except`

```python
try:
    number = int(input("Enter a whole number: "))
    if number % 2 == 0:
        print("Even")
    else:
        print("Odd")
except ValueError:
    print("Invalid input! Please enter digits only.")
```

**Sample run:**

```
Enter a whole number: hello
Invalid input! Please enter digits only.
```

#### Example 8: Different data types

```python
items = []

if items:
    print("Processing items...")
else:
    print("No items to process.")

price = 99.99
if price > 100.0:
    print("Expensive")
else:
    print("Affordable")
```

**Output:**

```
No items to process.
Affordable
```

### 4.6 `if` vs `if-else`

| Feature | `if` | `if-else` |
|---|---|---|
| Number of paths | 1 (run or skip) | 2 (one always runs) |
| When condition is false | Nothing happens | The `else` block runs |
| Use case | Optional action | Two mutually exclusive outcomes |

**Two separate `if` statements are not the same as `if-else`:**

```python
n = 10

# Version A: two independent ifs
if n > 5:
    print("Big")
if n <= 5:
    print("Small")

# Version B: if-else
if n > 5:
    print("Big")
else:
    print("Small")
```

**Output (both versions print the same thing):**

```
Big
Big
```

They give the same result here, but Version A evaluates **both** conditions every time, while Version B evaluates only one. If the code inside the first `if` changed `n`, Version A could even print both messages.

### 4.7 Real-World Use Cases

| Scenario | Logic |
|---|---|
| Login system | Correct credentials → dashboard, else → error |
| Exam result | `marks >= 40` → Pass, else → Fail |
| Shipping fee | `order_total >= 500` → free shipping, else → charge fee |
| Payment | Balance sufficient → proceed, else → decline |
| Feature flag | `is_premium` → show feature, else → show upgrade prompt |

### 4.8 Important Points / Rules

- `else` has **no condition**. Writing `else x > 5:` is a SyntaxError.
- `else` is **optional**, but it can only appear once and must be last.
- `else` must align with its `if`.
- `else` is the "everything not covered by the `if`" case.
- Only **one** of the two blocks ever runs.

### 4.9 Common Mistakes

| Mistake | Problem | Fix |
|---|---|---|
| Adding a condition to `else` | `else n < 5:` → SyntaxError | Use `elif n < 5:` |
| Misaligned `else` | `else` indented differently from `if` → SyntaxError | Align `else` with `if` |
| Forgetting the colon after `else` | SyntaxError | Write `else:` |
| Duplicate logic in both blocks | Repeated code | Move shared code outside the `if-else` |
| Putting code between `if` block and `else` | SyntaxError | Keep `else` immediately after the `if` block |

### 4.10 Best Practices

- Put the **most likely** or **simplest** case first for readability.
- Avoid an empty `else` that only has `pass`. Just omit the `else`.
- Move common statements **out** of the branches:

  ```python
  # Repetitive
  if score >= 40:
      print("Result declared")
      print("Pass")
  else:
      print("Result declared")
      print("Fail")

  # Better
  print("Result declared")
  if score >= 40:
      print("Pass")
  else:
      print("Fail")
  ```

### Key Takeaways

- `if-else` handles **both** outcomes of a condition, and exactly one block runs.
- `else` never has its own condition.
- Two separate `if`s are **not** equivalent to `if-else`.
- Normalize user input (`strip()`, `lower()`) and validate types before comparing.

---

## 5. The `if-elif-else` Ladder

### 5.1 Definition

The **`if-elif-else` statement** (also called an **if-elif ladder**) lets you test **multiple conditions in sequence**. Python checks them from top to bottom and runs the block of the **first condition that is true**. If none are true, the optional `else` block runs. `elif` is short for "else if".

### 5.2 Purpose / Why It Is Used

- When there are **more than two** possible outcomes.
- To categorize values into ranges or types (grades, age groups, tax slabs, ratings).
- To avoid deep nesting when choosing among several options.

### 5.3 Syntax

```python
if condition1:
    # runs if condition1 is True
elif condition2:
    # runs if condition1 is False and condition2 is True
elif condition3:
    # runs if the previous conditions are False and condition3 is True
else:
    # runs if all conditions above are False
```

| Part | Description |
|---|---|
| `if` | Starts the ladder (exactly one) |
| `elif` | Zero or more; each has its own condition |
| `else` | Optional; at most one; must be last; has no condition |

### 5.4 Flow of Execution

1. Evaluate the `if` condition. If `True`, run its block and **exit the whole ladder**.
2. Otherwise, evaluate the first `elif`. If `True`, run it and exit.
3. Continue down the ladder.
4. If nothing matched, run `else` (if present).

> **Note:** **At most one** block in the entire ladder runs. Once a match is found, the remaining conditions are **not even evaluated**.

### 5.5 Examples

#### Example 1: Grading system

```python
marks = 82

if marks >= 90:
    grade = "A+"
elif marks >= 80:
    grade = "A"
elif marks >= 70:
    grade = "B"
elif marks >= 60:
    grade = "C"
elif marks >= 40:
    grade = "D"
else:
    grade = "F"

print(f"Marks: {marks}, Grade: {grade}")
```

**Output:**

```
Marks: 82, Grade: A
```

**Explanation:** `82 >= 90` is false. `82 >= 80` is true, so grade `"A"` is assigned and the rest of the ladder is skipped.

#### Example 2: User input with a range check

```python
marks = int(input("Enter marks (0-100): "))

if marks < 0 or marks > 100:
    print("Invalid marks!")
elif marks >= 90:
    print("Grade A")
elif marks >= 75:
    print("Grade B")
elif marks >= 50:
    print("Grade C")
else:
    print("Fail")
```

**Sample runs:**

```
Enter marks (0-100): 150
Invalid marks!
```

```
Enter marks (0-100): 75
Grade B
```

```
Enter marks (0-100): 0
Fail
```

> **Tip:** Put **validation checks first**. That way, invalid data never falls into a valid-looking branch.

#### Example 3: Day of the week category

```python
day = input("Enter a day: ").strip().capitalize()

if day in ("Saturday", "Sunday"):
    print("Weekend - time to relax!")
elif day in ("Monday", "Tuesday", "Wednesday", "Thursday", "Friday"):
    print("Weekday - time to work.")
else:
    print("That is not a valid day.")
```

**Sample run:**

```
Enter a day: saturday
Weekend - time to relax!
```

#### Example 4: Age groups

```python
age = 45

if age < 0:
    print("Invalid age")
elif age < 13:
    print("Child")
elif age < 20:
    print("Teenager")
elif age < 60:
    print("Adult")
else:
    print("Senior citizen")
```

**Output:**

```
Adult
```

**Explanation:** Because conditions run in order, each `elif` only needs the **upper bound**. By the time we reach `age < 20`, we already know `age >= 13`.

#### Example 5: Simple calculator

```python
a = 20
b = 5
op = "/"

if op == "+":
    print(a + b)
elif op == "-":
    print(a - b)
elif op == "*":
    print(a * b)
elif op == "/":
    if b != 0:
        print(a / b)
    else:
        print("Cannot divide by zero")
else:
    print("Unknown operator")
```

**Output:**

```
4.0
```

**Explanation:** This also shows a small nested `if` inside an `elif` to guard against division by zero (nesting is covered in Section 6). Note that `/` always returns a `float` in Python.

#### Example 6: Electricity bill slabs (real-world)

```python
units = 250

if units <= 100:
    bill = units * 1.5
elif units <= 200:
    bill = 100 * 1.5 + (units - 100) * 2.5
else:
    bill = 100 * 1.5 + 100 * 2.5 + (units - 200) * 4

print(f"Units: {units}, Bill: {bill}")
```

**Output:**

```
Units: 250, Bill: 600.0
```

**Explanation:** 100 × 1.5 = 150, plus 100 × 2.5 = 250, plus 50 × 4 = 200, for a total of 600.

#### Example 7: The order of conditions matters (common bug)

```python
marks = 95

# WRONG ORDER
if marks >= 40:
    print("Grade D")
elif marks >= 60:
    print("Grade C")
elif marks >= 90:
    print("Grade A")
```

**Output:**

```
Grade D
```

**Explanation:** `95 >= 40` is true **first**, so Python stops there and the later, more specific conditions are never checked. Always order conditions from **most restrictive to least restrictive**, or use non-overlapping ranges.

**Corrected version:**

```python
marks = 95

if marks >= 90:
    print("Grade A")
elif marks >= 60:
    print("Grade C")
elif marks >= 40:
    print("Grade D")
```

**Output:**

```
Grade A
```

#### Example 8: Handling invalid input safely

```python
try:
    temp = float(input("Enter temperature in °C: "))
except ValueError:
    print("Please enter a valid number.")
else:
    if temp < 0:
        print("Freezing")
    elif temp < 15:
        print("Cold")
    elif temp < 30:
        print("Pleasant")
    else:
        print("Hot")
```

**Sample runs:**

```
Enter temperature in °C: 22.5
Pleasant
```

```
Enter temperature in °C: warm
Please enter a valid number.
```

### 5.6 `elif` Ladder vs Multiple Independent `if` Statements

This is a very common source of confusion.

```python
marks = 85

# Ladder: only ONE branch runs
if marks >= 80:
    print("Distinction")
elif marks >= 60:
    print("First class")
elif marks >= 40:
    print("Pass")

print("---")

# Independent ifs: EVERY true condition runs
if marks >= 80:
    print("Distinction")
if marks >= 60:
    print("First class")
if marks >= 40:
    print("Pass")
```

**Output:**

```
Distinction
---
Distinction
First class
Pass
```

| Feature | `if-elif-else` ladder | Multiple independent `if`s |
|---|---|---|
| Conditions checked | Stops at the first true one | All are checked |
| Blocks that can run | **At most one** | **Zero, one, or many** |
| Use when | Options are mutually exclusive | Conditions are independent |
| Efficiency | Fewer checks | More checks |

**Independent `if`s are correct when several things can be true together:**

```python
age = 25
has_license = True

if age >= 18:
    print("Can vote")
if has_license:
    print("Can drive")
```

**Output:**

```
Can vote
Can drive
```

### 5.7 `if-else` vs `if-elif-else`

| Aspect | `if-else` | `if-elif-else` |
|---|---|---|
| Number of outcomes | 2 | 3 or more |
| Conditions written | 1 | 2 or more |
| Typical use | Yes/no decisions | Categorization, multi-way choices |

### 5.8 Real-World Use Cases

| Scenario | Categories |
|---|---|
| Grade calculation | A / B / C / D / F |
| Income tax slabs | Different rates per range |
| Traffic light logic | Red / Yellow / Green |
| Menu-driven programs | Option 1 / 2 / 3 / Exit |
| Shipping cost tiers | Based on weight ranges |
| HTTP status handling | 200 / 404 / 500 |

### 5.9 Important Points / Rules

- Only the **first** true condition's block runs.
- You can have **any number** of `elif` blocks.
- `else` is optional and must come **last**.
- Every `elif` needs a **condition** and a **colon**.
- The `elif` keyword is spelled exactly `elif`, not `else if` or `elseif`.
- For simple value-to-action mapping, consider a dictionary or a `match` statement (Python 3.10+) instead of a very long ladder.

### 5.10 Common Mistakes

| Mistake | Example | Fix |
|---|---|---|
| Wrong keyword | `else if x > 5:` (SyntaxError) | `elif x > 5:` |
| Wrong order of conditions | Broad range before narrow range | Order most specific to least specific |
| Using independent `if`s when exclusivity is needed | Multiple messages print | Use `elif` |
| Overlapping conditions | `>= 50` and `<= 50` both cover 50 | Design boundaries carefully |
| Forgetting validation | Negative marks give "Fail" | Validate first |
| Putting a condition on `else` | `else marks < 40:` | Remove it, or use `elif` |

> **Warning:** Boundary values are a classic source of bugs. Always ask: "Which branch handles exactly `40`? Exactly `100`? Exactly `0`?"

### 5.11 Best Practices

- Order conditions so that **validation comes first**, then **specific to general**.
- Keep each branch short. Move long logic into functions.
- Always include an `else` when unexpected values are possible, to catch them explicitly.
- If a ladder grows beyond about 6 to 8 branches comparing one variable to constants, consider a dictionary lookup:

  ```python
  operations = {
      "+": lambda a, b: a + b,
      "-": lambda a, b: a - b,
      "*": lambda a, b: a * b,
  }
  op = "+"
  print(operations[op](6, 3))
  ```

  **Output:**

  ```
  9
  ```

### Key Takeaways

- `if-elif-else` handles **three or more** outcomes and stops at the **first** true condition.
- **Order matters**: put validation and the most specific conditions first.
- Use `elif` for mutually exclusive choices, and separate `if`s for independent checks.
- Design range boundaries carefully to avoid gaps and overlaps.

---

## 6. Nested `if` Statements

### 6.1 Definition

A **nested `if`** is an `if` (or `if-else` / `if-elif-else`) statement **placed inside** another `if`, `elif`, or `else` block. The inner condition is only evaluated if the outer condition allows execution to reach it.

### 6.2 Purpose / Why It Is Used

- When a decision **depends on the result of a previous decision**.
- To model **hierarchical** or **dependent** checks (e.g., "is the user logged in? If yes, is the user an admin?").
- To validate step by step, where later checks make sense only if earlier ones pass.

### 6.3 Syntax

```python
if outer_condition:
    # outer block
    if inner_condition:
        # runs only if BOTH outer and inner conditions are True
    else:
        # runs if outer is True but inner is False
else:
    # runs if outer condition is False
```

Nesting can go inside `elif` and `else` blocks as well, and to any depth (though deep nesting is discouraged).

### 6.4 Flow of Execution

1. Evaluate the **outer** condition.
2. If `False`, skip the entire outer block (inner conditions are **never evaluated**).
3. If `True`, enter the block and evaluate the **inner** condition.
4. Continue the same way for deeper levels.

### 6.5 Examples

#### Example 1: Basic nested `if`

```python
age = 25
has_id = True

if age >= 18:
    print("Age requirement met.")
    if has_id:
        print("Entry allowed.")
    else:
        print("Please show your ID.")
else:
    print("Entry denied: underage.")
```

**Output:**

```
Age requirement met.
Entry allowed.
```

**Explanation:** The outer condition passes. The inner condition passes as well, so "Entry allowed." prints.

#### Example 2: Different combinations

Using the same code, here are all the possible outcomes:

| `age` | `has_id` | Output |
|---|---|---|
| 25 | True | `Age requirement met.` → `Entry allowed.` |
| 25 | False | `Age requirement met.` → `Please show your ID.` |
| 15 | True | `Entry denied: underage.` |
| 15 | False | `Entry denied: underage.` |

> **Note:** In the last two rows, `has_id` is never checked, because the outer condition already failed.

#### Example 3: Login with role check (user input)

```python
username = input("Username: ")
password = input("Password: ")

if username == "admin":
    if password == "secret":
        print("Welcome, Admin!")
    else:
        print("Wrong password.")
else:
    print("Unknown user.")
```

**Sample runs:**

```
Username: admin
Password: secret
Welcome, Admin!
```

```
Username: admin
Password: abc
Wrong password.
```

```
Username: guest
Password: anything
Unknown user.
```

#### Example 4: Largest of three numbers

```python
a, b, c = 12, 45, 30

if a >= b:
    if a >= c:
        print(f"Largest is {a}")
    else:
        print(f"Largest is {c}")
else:
    if b >= c:
        print(f"Largest is {b}")
    else:
        print(f"Largest is {c}")
```

**Output:**

```
Largest is 45
```

**Explanation:** First compare `a` and `b`, then compare the winner with `c`. (In real code, `max(a, b, c)` is simpler, but this shows how nesting works.)

#### Example 5: Triangle validity and type

```python
a, b, c = 5, 5, 8

if a > 0 and b > 0 and c > 0:
    if a + b > c and a + c > b and b + c > a:
        if a == b == c:
            print("Equilateral triangle")
        elif a == b or b == c or a == c:
            print("Isosceles triangle")
        else:
            print("Scalene triangle")
    else:
        print("Sides do not form a triangle.")
else:
    print("Sides must be positive.")
```

**Output:**

```
Isosceles triangle
```

**Explanation:** Three levels of checks: positive sides → triangle inequality → type of triangle.

#### Example 6: ATM withdrawal (real-world)

```python
balance = 5000
pin_correct = True
amount = 3000

if pin_correct:
    if amount > 0:
        if amount <= balance:
            balance -= amount
            print(f"Withdrawal successful. Remaining balance: {balance}")
        else:
            print("Insufficient balance.")
    else:
        print("Enter a valid amount.")
else:
    print("Incorrect PIN.")
```

**Output:**

```
Withdrawal successful. Remaining balance: 2000
```

#### Example 7: Nested `if` inside `elif`

```python
score = 85
attendance = 70

if score >= 90:
    print("Excellent")
elif score >= 60:
    if attendance >= 75:
        print("Passed")
    else:
        print("Passed but short of attendance")
else:
    print("Failed")
```

**Output:**

```
Passed but short of attendance
```

#### Example 8: Edge case with invalid input

```python
raw = input("Enter your age: ")

if raw.isdigit():
    age = int(raw)
    if age >= 18:
        print("Adult")
    else:
        print("Minor")
else:
    print("Invalid input. Please enter a whole number.")
```

**Sample run:**

```
Enter your age: -5
Invalid input. Please enter a whole number.
```

**Explanation:** `"-5".isdigit()` is `False` because of the minus sign, so the outer `else` handles it.

### 6.6 Nested `if` vs Combined Conditions with `and`

When there is **no separate action** for the outer-only case, a nested `if` can often be flattened using `and`.

```python
age = 25
has_id = True

# Nested version
if age >= 18:
    if has_id:
        print("Entry allowed.")

# Flattened version (equivalent)
if age >= 18 and has_id:
    print("Entry allowed.")
```

**Output (both versions):**

```
Entry allowed.
Entry allowed.
```

| Aspect | Nested `if` | Combined with `and` |
|---|---|---|
| Different messages per failure | Easy | Hard (need extra logic) |
| Readability for simple checks | More indentation | Cleaner |
| Step-by-step dependent logic | Natural | Awkward |
| When the inner check depends on the outer | Natural fit | Short-circuit `and` also works |

> **Tip:** Use **nesting** when each level needs its **own message or action**. Use **`and`** when you only care whether *all* conditions hold.

### 6.7 Nested `if` vs `elif`

| Situation | Best choice |
|---|---|
| Choosing **one of several independent options** for the same variable | `elif` ladder |
| Second decision **depends on** the first one being true | Nested `if` |

### 6.8 Real-World Use Cases

| Scenario | Nested logic |
|---|---|
| Online checkout | Logged in? → Cart not empty? → Payment valid? |
| Bank/ATM | PIN correct? → Amount valid? → Sufficient funds? |
| Admission systems | Passed exam? → Meets cutoff? → Seats available? |
| Access control | Authenticated? → Authorized for this resource? |
| Game logic | Player alive? → Has key? → Door unlocked? |

### 6.9 Important Points / Rules

- Each nested level needs **additional indentation** (4 spaces).
- An `else` belongs to the **nearest `if` at the same indentation level**. Indentation, not position, decides the pairing.
- Any block (`if`, `elif`, `else`) can contain a nested `if`.
- Inner conditions are evaluated **only** if the execution reaches them.
- Python has no hard limit on nesting depth, but readability suffers quickly.

### 6.10 Common Mistakes

| Mistake | Effect | Fix |
|---|---|---|
| Wrong indentation of the inner `else` | It pairs with the wrong `if` | Align each `else` with its own `if` |
| Excessive nesting (4+ levels) | Hard to read and debug | Use guard clauses, `and`, or functions |
| Forgetting that inner code may never run | Logic bugs | Trace with sample values |
| Duplicating checks in outer and inner blocks | Redundant code | Simplify conditions |
| Using nested `if` where `elif` is enough | Unnecessarily complex | Use an `elif` ladder |

**Indentation changes meaning:**

```python
x = 10
y = 3

# Version A: else pairs with the INNER if
if x > 5:
    if y > 5:
        print("Both big")
    else:
        print("x big, y small")

# Version B: else pairs with the OUTER if
if x > 5:
    if y > 5:
        print("Both big")
else:
    print("x is small")
```

**Output:**

```
x big, y small
```

*(Version B prints nothing here, because `x > 5` is true, so the outer `else` is skipped.)*

### 6.11 Best Practices

- **Avoid deep nesting.** Prefer at most 2 to 3 levels.
- Use **guard clauses** (early exit) to flatten code inside functions:

  ```python
  def withdraw(balance, amount, pin_correct):
      if not pin_correct:
          return "Incorrect PIN."
      if amount <= 0:
          return "Enter a valid amount."
      if amount > balance:
          return "Insufficient balance."
      return f"Withdrawn {amount}. Remaining: {balance - amount}"

  print(withdraw(5000, 3000, True))
  print(withdraw(5000, 9000, True))
  print(withdraw(5000, 1000, False))
  ```

  **Output:**

  ```
  Withdrawn 3000. Remaining: 2000
  Insufficient balance.
  Incorrect PIN.
  ```

- Use meaningful variable names for compound conditions.
- Combine conditions with `and` when there is no separate action for each level.

### Key Takeaways

- A nested `if` is an `if` **inside another block**, used when one decision **depends** on another.
- Inner conditions only run when the outer condition lets execution reach them.
- The `else` pairs with the nearest `if` at the **same indentation**.
- Prefer flattening (`and`, guard clauses) when nesting gets deep.

---

## 7. The Ternary Operator

### 7.1 Definition

The **ternary operator** (also called the **conditional expression** or **inline if-else**) is a compact way to choose **between two values** based on a condition, all in **a single line**.

It is called *ternary* because it takes **three operands**: a condition, a value for true, and a value for false.

### 7.2 Purpose / Why It Is Used

- To write **simple two-way decisions** concisely.
- To **assign a value** to a variable based on a condition.
- To embed a decision **inside an expression** (in `print`, `return`, function arguments, f-strings, list comprehensions).

### 7.3 Syntax

```python
value_if_true if condition else value_if_false
```

| Part | Description |
|---|---|
| `value_if_true` | Result when the condition is `True` |
| `condition` | Expression evaluated first |
| `value_if_false` | Result when the condition is `False` |

> **Note:** Unlike C, Java, or JavaScript (`condition ? a : b`), Python's ternary puts the **condition in the middle**.

### 7.4 Flow of Execution

1. Python evaluates the **condition** first.
2. If `True`, only `value_if_true` is evaluated and returned.
3. If `False`, only `value_if_false` is evaluated and returned.

Only **one** of the two value expressions is evaluated (lazy evaluation).

### 7.5 Examples

#### Example 1: Basic usage

```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)
```

**Output:**

```
Adult
```

**Equivalent `if-else`:**

```python
if age >= 18:
    status = "Adult"
else:
    status = "Minor"
```

#### Example 2: Even or odd

```python
n = 7
print("Even" if n % 2 == 0 else "Odd")
```

**Output:**

```
Odd
```

#### Example 3: Maximum of two numbers

```python
a, b = 15, 27
largest = a if a > b else b
print(f"Largest: {largest}")
```

**Output:**

```
Largest: 27
```

#### Example 4: User input

```python
marks = int(input("Enter marks: "))
result = "Pass" if marks >= 40 else "Fail"
print(f"Result: {result}")
```

**Sample runs:**

```
Enter marks: 65
Result: Pass
```

```
Enter marks: 40
Result: Pass
```

```
Enter marks: 39
Result: Fail
```

#### Example 5: Inside an f-string

```python
items = 1
print(f"You have {items} item{'s' if items != 1 else ''} in your cart.")

items = 3
print(f"You have {items} item{'s' if items != 1 else ''} in your cart.")
```

**Output:**

```
You have 1 item in your cart.
You have 3 items in your cart.
```

> **Tip:** This is a very common real-world use: correct singular and plural forms.

#### Example 6: Different data types

```python
# Numbers
discount = 0.10 if 1200 > 1000 else 0.0
print(discount)

# Strings
greeting = "Good morning" if 9 < 12 else "Good afternoon"
print(greeting)

# Lists
data = []
display = data if data else ["No data"]
print(display)

# None handling (default value)
username = None
name = username if username is not None else "Guest"
print(name)
```

**Output:**

```
0.1
Good morning
['No data']
Guest
```

#### Example 7: Inside a function return

```python
def absolute(x):
    return x if x >= 0 else -x

print(absolute(-8))
print(absolute(5))
print(absolute(0))
```

**Output:**

```
8
5
0
```

#### Example 8: In a list comprehension

```python
numbers = [1, 2, 3, 4, 5, 6]
labels = ["even" if n % 2 == 0 else "odd" for n in numbers]
print(labels)
```

**Output:**

```
['odd', 'even', 'odd', 'even', 'odd', 'even']
```

#### Example 9: Nested (chained) ternary

```python
marks = 72

grade = "A" if marks >= 80 else "B" if marks >= 60 else "C" if marks >= 40 else "F"
print(grade)
```

**Output:**

```
B
```

**Explanation:** It reads as *"A if marks ≥ 80, otherwise (B if marks ≥ 60, otherwise (C if marks ≥ 40, otherwise F))"*. This is equivalent to an `if-elif-else` ladder.

> **Warning:** Chained ternaries get hard to read quickly. Beyond **two levels**, use `if-elif-else` instead.

#### Example 10: Edge cases

```python
# 1. Missing else is a SyntaxError
# result = "Yes" if True        # SyntaxError

# 2. Truthiness works as the condition
count = 0
print("Empty" if not count else "Has items")

# 3. Both value expressions can be function calls (only one runs)
def yes():
    print("yes() called")
    return "Y"

def no():
    print("no() called")
    return "N"

print(yes() if 5 > 3 else no())
```

**Output:**

```
Empty
yes() called
Y
```

**Explanation:** `no()` is never called, which confirms that only the chosen branch is evaluated.

### 7.6 Ternary Operator vs `if-else` Statement

| Feature | Ternary operator | `if-else` statement |
|---|---|---|
| Type | **Expression** (produces a value) | **Statement** (performs actions) |
| Lines | Single line | Multiple lines |
| Can be used inside other expressions | Yes | No |
| Can contain multiple statements per branch | No | Yes |
| `else` mandatory | **Yes** | No (optional) |
| Best for | Simple value selection | Complex logic, side effects |
| Readability with complex logic | Poor | Good |

**Only expressions are allowed in each branch, not statements:**

```python
# INVALID: an assignment is a statement, not an expression
# x = 5 if cond else (y = 3)     # SyntaxError

# Use if-else when you need multiple statements
if cond:
    total += 10
    print("Added")
else:
    print("Skipped")
```

### 7.7 Ternary vs Other "Tricks"

| Technique | Example | Verdict |
|---|---|---|
| Ternary operator | `x = a if cond else b` | Recommended |
| `and`/`or` trick | `x = cond and a or b` | Buggy if `a` is falsy (e.g., `0`, `""`) |
| Tuple indexing | `x = (b, a)[cond]` | Evaluates **both** `a` and `b`; less readable |

```python
# Why the and/or trick is unreliable
cond = True
a = 0            # falsy value
print(cond and a or "fallback")     # prints "fallback", not 0!
print(a if cond else "fallback")    # prints 0 (correct)
```

**Output:**

```
fallback
0
```

### 7.8 Real-World Use Cases

| Scenario | Example |
|---|---|
| Default values | `name = user_name if user_name else "Guest"` |
| Pluralization | `"s" if count != 1 else ""` |
| UI labels | `"Logout" if logged_in else "Login"` |
| Discount or fee | `fee = 0 if total >= 500 else 40` |
| Clamping or fallback | `value = x if x <= limit else limit` |
| Data cleaning | `[x if x is not None else 0 for x in data]` |

### 7.9 Important Points / Rules

- The `else` part is **mandatory**.
- Both branches must be **expressions**, not statements.
- Only **one** branch is evaluated.
- The ternary has **low precedence**, so use parentheses when combining it with other operators.
- It can be nested, but this is rarely a good idea.
- It is available in Python 2.5+ and all Python 3 versions.

### 7.10 Common Mistakes

| Mistake | Problem | Fix |
|---|---|---|
| Omitting `else` | SyntaxError | Always include `else` |
| Using C-style syntax `cond ? a : b` | SyntaxError | `a if cond else b` |
| Overusing nested ternaries | Unreadable | Use `if-elif-else` |
| Putting statements in a branch | SyntaxError | Use a regular `if-else` |
| Ignoring precedence | Unexpected output | Add parentheses |

**Precedence pitfall:**

```python
x = 5
print("Big" if x > 3 else "Small" + "!")     # "!" only attaches to "Small"
print(("Big" if x > 3 else "Small") + "!")    # "!" attaches to the result
```

**Output:**

```
Big
Big!
```

### 7.11 Best Practices

- Use the ternary only for **short, simple** decisions that fit comfortably on one line.
- Keep the condition **simple** and **positive** (avoid `not` where possible).
- For anything with side effects (printing, modifying state, multiple steps), use `if-else`.
- Wrap in parentheses when it improves clarity:

  ```python
  label = ("Pass" if marks >= 40 else "Fail")
  ```

- If the line exceeds about 79 characters, switch to a regular `if-else`.

### Key Takeaways

- The ternary operator is `value_if_true if condition else value_if_false`.
- It is an **expression** that returns a value, so it can appear inside other expressions.
- `else` is **mandatory**; nesting is possible but discouraged.
- Prefer `if-else` for complex logic. Avoid `and`/`or` and tuple-indexing tricks.

---

## 8. How the Topics Connect

All five constructs answer the same question, "*which code should run?*", at different levels of complexity.

### 8.1 Choosing the Right Construct

| Situation | Best construct |
|---|---|
| Do something **only if** a condition holds | `if` |
| Two mutually exclusive outcomes (statements) | `if-else` |
| Three or more mutually exclusive outcomes | `if-elif-else` |
| A decision that **depends on** another decision | Nested `if` |
| Pick **one of two values** in a single expression | Ternary operator |

### 8.2 Side-by-Side Comparison

The same problem solved five different ways: *classify a number*.

```python
n = 15

# 1. if: only handle the special case
if n > 10:
    print("Greater than 10")

# 2. if-else: two outcomes
if n > 10:
    print("Greater than 10")
else:
    print("10 or less")

# 3. if-elif-else: three outcomes
if n > 10:
    print("Greater than 10")
elif n == 10:
    print("Exactly 10")
else:
    print("Less than 10")

# 4. nested if: dependent decisions
if n > 0:
    if n % 2 == 0:
        print("Positive even")
    else:
        print("Positive odd")
else:
    print("Zero or negative")

# 5. ternary: single-line value selection
print("Greater than 10" if n > 10 else "10 or less")
```

**Output:**

```
Greater than 10
Greater than 10
Greater than 10
Positive odd
Greater than 10
```

### 8.3 Feature Comparison Table

| Feature | `if` | `if-else` | `if-elif-else` | Nested `if` | Ternary |
|---|:---:|:---:|:---:|:---:|:---:|
| Number of outcomes | 1 (or none) | 2 | 3+ | Many (dependent) | 2 |
| Multiple statements per branch | Yes | Yes | Yes | Yes | No |
| Used inside an expression | No | No | No | No | Yes |
| `else` required | No | It is the `else` | No (optional) | No | Yes |
| Conditions evaluated | 1 | 1 | Up to *n* (stops at first true) | Depends on outer results | 1 |
| Readability with many cases | Good | Good | Good | Worse with depth | Poor if nested |

### 8.4 Progression of Complexity

1. **`if`**: a single optional action.
2. **`if-else`**: adds a second path.
3. **`if-elif-else`**: extends to many paths.
4. **Nested `if`**: adds *dependent* decisions.
5. **Ternary**: a shorthand for the simple two-way case.

> **Tip:** Start with the simplest construct that solves the problem. Move to a more complex one only when necessary.

### Key Takeaways

- Every construct is a variation of "evaluate condition(s), then choose".
- Use `elif` for mutually exclusive options, nesting for dependent ones, and ternary for simple value selection.
- Simplicity and readability should drive the choice.

---

## 9. Overall Summary

- **Control statements** change the default sequential flow. **Conditional statements** choose code paths based on conditions.
- Conditions are built from **comparison operators** (`==`, `!=`, `<`, `>`, `<=`, `>=`) and **logical operators** (`and`, `or`, `not`). Any value can be used as a condition through **truthiness**.
- **`if`** runs a block only when the condition is true.
- **`if-else`** guarantees that exactly one of two blocks runs.
- **`if-elif-else`** handles many mutually exclusive cases and stops at the **first** match. Order matters.
- **Nested `if`** handles decisions that depend on earlier decisions. Keep nesting shallow with `and` and guard clauses.
- The **ternary operator** (`a if cond else b`) is a concise expression form for simple two-way choices.
- Python relies on **indentation** and **colons**. Mistakes here cause `SyntaxError` or `IndentationError`.
- Always test **boundary values**, **invalid input**, and **empty or `None` values**.

---

## 10. Quick Revision / Cheat Sheet

### 10.1 Syntax Reference

| Construct | Syntax |
|---|---|
| `if` | `if cond:` → block |
| `if-else` | `if cond:` → block, `else:` → block |
| `if-elif-else` | `if c1:` … `elif c2:` … `else:` … |
| Nested `if` | An `if` inside any block |
| Ternary | `x = a if cond else b` |

### 10.2 Operator Reference

| Type | Operators |
|---|---|
| Comparison | `==` `!=` `>` `<` `>=` `<=` |
| Logical | `and` `or` `not` |
| Membership | `in` `not in` |
| Identity | `is` `is not` |

### 10.3 Falsy Values (memorize these)

`False`, `None`, `0`, `0.0`, `""`, `[]`, `()`, `{}`, `set()`

### 10.4 Rules at a Glance

- Colon `:` after `if`, `elif`, and `else`.
- Use **4 spaces** of indentation; be consistent.
- `else` has **no condition**; `elif` **must** have one.
- The ladder runs **only the first true branch**.
- Ternary **requires** `else`.
- `=` assigns; `==` compares.
- `input()` returns a **string**. Convert before numeric comparison.
- Use `is None` rather than `== None`.

### 10.5 Decision Guide

```
One optional action?               → if
Two outcomes?                      → if-else
Three or more outcomes?            → if-elif-else
Second check depends on the first? → nested if
Simple value selection in a line?  → ternary
```

### 10.6 Top Mistakes to Avoid

1. `if x = 5:` instead of `if x == 5:`
2. `else if` instead of `elif`
3. Wrong order in an `elif` ladder
4. `if x == 1 or 2:` (always true)
5. Missing colon or wrong indentation
6. Ternary without `else`
7. Deeply nested `if` blocks that could be flattened
8. Comparing `input()` text directly with numbers

---

## 11. Common Interview Questions

**1. What is the difference between `if-else` and `if-elif-else`?**
`if-else` supports two outcomes, while `if-elif-else` supports three or more by testing conditions in sequence. Only one block runs in each.

**2. Does Python have a `switch` statement?**
Python 3.10 added structural pattern matching with `match-case`. Before that, `if-elif-else` chains or dictionary lookups were used.

**3. What is the difference between `elif` and multiple `if` statements?**
In an `elif` ladder, once a condition is true the rest are skipped. With separate `if`s, every condition is evaluated independently, so multiple blocks may run.

**4. What are truthy and falsy values? Give examples.**
Falsy: `False`, `None`, `0`, `0.0`, `""`, `[]`, `{}`, `()`, `set()`. Almost everything else is truthy, including `"0"` and `"False"` as strings.

**5. What is short-circuit evaluation?**
In `A and B`, if `A` is false, `B` is not evaluated. In `A or B`, if `A` is true, `B` is not evaluated. It prevents errors like division by zero: `if b != 0 and a / b > 2`.

**6. What is the ternary operator in Python and what is its syntax?**
A one-line conditional expression: `value_if_true if condition else value_if_false`.

**7. Can we use the ternary operator without `else`?**
No. `else` is mandatory, or a `SyntaxError` occurs.

**8. When should you avoid the ternary operator?**
When logic is complex, requires multiple statements, or would need nested ternaries. Use `if-else` for readability.

**9. What is the difference between `==` and `is`?**
`==` compares **values**; `is` compares **object identity** (same object in memory). Use `is` mainly with `None`.

**10. What happens if you write `if x == 1 or 2:`?**
It is parsed as `(x == 1) or 2`. Since `2` is truthy, the condition is always true. The correct forms are `x == 1 or x == 2` or `x in (1, 2)`.

**11. What is a nested `if` and when is it useful?**
An `if` inside another `if` block. Useful when a decision depends on a prior decision, such as login → role → permission.

**12. How can you reduce deep nesting?**
Use logical operators (`and`), guard clauses with early `return`, extract functions, or use dictionaries or `match`.

**13. Does an `if` block create a new scope in Python?**
No. Variables defined inside an `if` block remain accessible after it, in the enclosing function or module scope.

**14. What is the output?**

```python
x = 0
if x:
    print("A")
elif x == 0:
    print("B")
else:
    print("C")
```

Answer: `B`, because `0` is falsy (so `A` is skipped) but `x == 0` is true.

**15. Is an empty `else` block allowed?**
No. A block must contain at least one statement. Use `pass` if you truly need a placeholder, though it is usually better to omit the `else`.

---

## 12. Practice Questions / Exercises

### Section A: `if` block

1. Read a number and print `"Positive"` only if it is greater than zero.
2. Read a person's age and print `"Eligible to vote"` if the age is 18 or above.
3. Check whether a string entered by the user is empty. Print `"Empty input"` if it is.

### Section B: `if-else`

4. Determine whether a number is even or odd.
5. Read a year and determine whether it is a leap year (test with 1900, 2000, 2023, 2024).
6. Ask for a username and password. Print `"Login successful"` or `"Login failed"` based on hard-coded credentials.
7. Read two numbers and print the larger one. Handle the case where they are equal.

### Section C: `if-elif-else`

8. Read marks (0 to 100) and print the grade using a scale of your choice. Reject values outside the range.
9. Read a number from 1 to 7 and print the day of the week. Print an error for other values.
10. Read a temperature and print `"Freezing"`, `"Cold"`, `"Pleasant"`, or `"Hot"`.
11. Build a calculator that takes two numbers and an operator (`+`, `-`, `*`, `/`) and prints the result. Handle division by zero and invalid operators.
12. Calculate an electricity bill based on slab rates (design your own slabs).

### Section D: Nested `if`

13. Read three numbers and find the largest using nested `if` statements.
14. Read three side lengths. Check whether they form a triangle, then classify it as equilateral, isosceles, or scalene.
15. Simulate an ATM: check the PIN, then check that the amount is positive, then check that the balance is sufficient.
16. Read a character. If it is a letter, check whether it is a vowel or a consonant; otherwise print `"Not a letter"`.

### Section E: Ternary operator

17. Rewrite Exercise 4 (even/odd) using a ternary expression.
18. Rewrite Exercise 7 (larger of two numbers) using a ternary expression.
19. Given a number of items in a cart, print `"1 item"` or `"N items"` correctly (singular/plural).
20. Given a list of numbers, create a new list where negatives become `0` and other numbers stay the same (use a ternary in a list comprehension).

### Section F: Conceptual and Debugging

21. Find and fix the errors:

    ```python
    x = 10
    if x = 10
    print("Ten")
    else if x > 5:
        print("Greater than five")
    ```

22. Predict the output, then run the code to verify:

    ```python
    n = 15
    if n > 5:
        print("A")
    if n > 10:
        print("B")
    elif n > 12:
        print("C")
    else:
        print("D")
    ```

23. Explain why this condition is a bug and fix it:

    ```python
    if color == "red" or "blue":
        print("Primary colour")
    ```

24. Convert this nested `if` into a single `if` using `and`:

    ```python
    if a > 0:
        if b > 0:
            print("Both positive")
    ```

25. Convert the following `if-elif-else` into a chained ternary and explain why you would or would not prefer the ternary version:

    ```python
    if marks >= 60:
        result = "First class"
    elif marks >= 40:
        result = "Pass"
    else:
        result = "Fail"
    ```

### Answers to Selected Questions

**Q21:** Corrected code:

```python
x = 10
if x == 10:
    print("Ten")
elif x > 5:
    print("Greater than five")
```

The errors were `=` instead of `==`, a missing colon, a missing indent on `print("Ten")`, and `else if` instead of `elif`.

**Q22:** Output is

```
A
B
```

Explanation: the first `if n > 5` is independent, so `A` prints. The second `if n > 10` starts a new statement: it is true, so `B` prints and its `elif` and `else` are skipped.

**Q23:** `"blue"` is a non-empty string and therefore always truthy, so the condition is always true. Fix: `if color == "red" or color == "blue":` or `if color in ("red", "blue"):`.

**Q24:** `if a > 0 and b > 0: print("Both positive")`

**Q25:** `result = "First class" if marks >= 60 else "Pass" if marks >= 40 else "Fail"`. It is acceptable for two levels, but the `if-elif-else` form is easier to read and extend, so prefer it as conditions grow.

---

*End of guide.*
