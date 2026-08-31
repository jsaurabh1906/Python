# Python Tuples, Sets, Dictionaries, and Mutability — Complete Reference Guide

## Overview

This guide covers four closely related areas of Python's data model:

- **Tuples** — ordered, immutable sequences
- **Sets** — unordered collections of unique, hashable elements, along with set algebra (union, intersection, difference) and the immutable `frozenset`
- **Dictionaries** — key-value mappings, including how keys and values work internally, what types are allowed, and how to manipulate dictionary data
- **Mutability and Immutability** — the core concept that ties everything together, explained through tuples, lists, and strings, followed by a deep walkthrough of **shallow vs. deep copying**

By the end of this document, you should understand not just *how* to use these data structures, but *why* they behave the way they do — particularly why some objects can be changed in place and others cannot, and how that affects copying behavior.

> **Note:** All code examples in this guide were executed and verified. The output shown under each example reflects the actual result of running that code in Python 3.

---

## Table of Contents

1. [Tuples](#1-tuples)
   - [1.1 Introduction to Tuples](#11-introduction-to-tuples)
   - [1.2 Basic Operations on Tuples](#12-basic-operations-on-tuples)
2. [Sets](#2-sets)
   - [2.1 Introduction to Sets](#21-introduction-to-sets)
   - [2.2 Basic Operations on Sets](#22-basic-operations-on-sets)
   - [2.3 Set Operations: Union, Intersection, Difference](#23-set-operations-union-intersection-difference)
   - [2.4 Frozenset](#24-frozenset)
3. [Dictionaries](#3-dictionaries)
   - [3.1 Introduction to Dictionaries](#31-introduction-to-dictionaries)
   - [3.2 Operations on Dictionaries: Updating, Deleting, and Others](#32-operations-on-dictionaries-updating-deleting-and-others)
   - [3.3 Working with Keys and Values in Depth](#33-working-with-keys-and-values-in-depth)
   - [3.4 Allowed and Not Allowed Types for Keys and Values](#34-allowed-and-not-allowed-types-for-keys-and-values)
4. [Mutability and Immutability](#4-mutability-and-immutability)
   - [4.1 Core Concept](#41-core-concept)
   - [4.2 Mutability in Lists](#42-mutability-in-lists)
   - [4.3 Immutability in Tuples](#43-immutability-in-tuples)
   - [4.4 Immutability in Strings](#44-immutability-in-strings)
   - [4.5 The Special Case: Mutable Objects Inside Immutable Containers](#45-the-special-case-mutable-objects-inside-immutable-containers)
5. [Shallow Copy vs Deep Copy — Deep Walkthrough](#5-shallow-copy-vs-deep-copy--deep-walkthrough)
6. [Summary](#6-summary)
7. [Quick Revision / Cheat Sheet](#7-quick-revision--cheat-sheet)
8. [Common Interview Questions](#8-common-interview-questions)
9. [Practice Exercises](#9-practice-exercises)

---

## 1. Tuples

### 1.1 Introduction to Tuples

**Definition:**
A tuple is an ordered, **immutable** collection of items in Python. Once created, the elements of a tuple cannot be changed, added, or removed.

**Purpose / Why it is used:**
- To store a fixed collection of related values that should not change (e.g., coordinates, RGB colors, database records).
- To use as dictionary keys or set elements (since tuples are hashable if their contents are hashable), which lists cannot do.
- To signal intent — using a tuple tells other developers "this data is not meant to be modified."
- Slightly more memory-efficient and faster to iterate than lists in many cases.

**Syntax:**

```python
# Using parentheses
my_tuple = (1, 2, 3)

# Parentheses are optional (tuple packing)
my_tuple2 = 1, 2, 3

# Empty tuple
empty = ()

# Single-element tuple (comma is mandatory!)
single = (5,)
```

**Detailed Explanation:**
Tuples look similar to lists but behave very differently because of immutability. Internally, Python can optimize tuples more aggressively than lists because their size and content are fixed after creation.

A very common beginner mistake is creating a "tuple" with just parentheses and one value, like `(5)`. Without a trailing comma, Python treats this as a plain expression, not a tuple.

**Example:**

```python
t = (1, 2, 3, "four", 5.0)
print("tuple:", t)
print("len:", len(t))

t2 = (1,)
print("single element tuple:", t2, type(t2))

not_tuple = (1)
print("not a tuple:", not_tuple, type(not_tuple))
```

**Output:**

```
tuple: (1, 2, 3, 'four', 5.0)
len: 5
single element tuple: (1,) <class 'tuple'>
not a tuple: 1 <class 'int'>
```

**Real-world use cases:**
- Returning multiple values from a function (`return x, y`)
- Representing fixed records like `(latitude, longitude)` or `(r, g, b)`
- Using as dictionary keys for composite keys, e.g., `{(2024, 1): "January Sales"}`
- Unpacking function arguments and results

> **Note:** Tuples are **heterogeneous** — they can hold mixed data types like `(1, "text", 3.5, True)`.

> **Warning:** `(5)` is an `int`, not a tuple. You must write `(5,)` with a trailing comma to create a single-element tuple.

---

### 1.2 Basic Operations on Tuples

#### Creating and Accessing Tuples

```python
t = (10, 20, 30, 40, 50)
print(t[0])      # first element
print(t[-1])     # last element
print(t[1:4])    # slicing
print(t[::-1])   # reversed
```

**Output:**

```
10
50
(20, 30, 40)
(50, 40, 30, 20, 10)
```

#### Tuple Packing and Unpacking

```python
# Packing
person = "Saurabh", 30, "Pune"

# Unpacking
name, age, city = person
print(name, age, city)

# Unpacking with * (collects remaining items)
first, *rest = (1, 2, 3, 4)
print(first, rest)
```

**Output:**

```
Saurabh 30 Pune
1 [2, 3, 4]
```

> **Tip:** Tuple unpacking is widely used in `for` loops when iterating over `dict.items()`: `for key, value in my_dict.items():`.

#### Concatenation and Repetition

```python
a = (1, 2)
b = (3, 4)
print(a + b)     # concatenation
print(a * 3)     # repetition
```

**Output:**

```
(1, 2, 3, 4)
(1, 2, 1, 2, 1, 2)
```

#### Built-in Tuple Methods

Tuples support only **two** methods because they cannot be modified:

| Method | Description | Example | Output |
|---|---|---|---|
| `.count(x)` | Counts occurrences of `x` | `(1,2,2,3).count(2)` | `2` |
| `.index(x)` | Returns index of first occurrence of `x` | `(1,2,3).index(3)` | `2` |

```python
t = (1, 2, 3, "four", 5.0)
print(t.index("four"))
print(t.count(2))
```

**Output:**

```
3
1
```

#### Nested Tuples

```python
nested = (1, (2, 3), [4, 5])
print(nested)
print(nested[1][0])   # accessing inside nested tuple
```

**Output:**

```
(1, (2, 3), [4, 5])
2
```

#### Important Points / Rules

- Tuples are **ordered** — indexing and slicing work like lists.
- Tuples are **immutable** — you cannot reassign, add, or remove elements after creation.
- Tuples can contain **mutable objects** (like lists), and those inner objects *can* still be changed — only the tuple's own structure (the references it holds) is frozen.
- Tuples are **hashable** only if every element inside them is hashable, which makes them usable as dictionary keys or set elements.

#### Common Mistakes

- Forgetting the trailing comma for a single-element tuple: `(5)` is an int, not a tuple.
- Trying to modify a tuple directly: `t[0] = 100` raises `TypeError`.
- Assuming a tuple is fully "frozen" even when it holds mutable objects like lists.

#### Best Practices

- Use tuples for fixed, related data that shouldn't change (e.g., a point, a date).
- Prefer tuples over lists when you need a hashable, immutable sequence (e.g., as a dictionary key).
- Use named tuples (`collections.namedtuple`) when fields need to be self-documenting.

#### Comparison: Tuple vs List

| Feature | Tuple | List |
|---|---|---|
| Mutability | Immutable | Mutable |
| Syntax | `(1, 2, 3)` | `[1, 2, 3]` |
| Performance | Slightly faster, less memory | Slightly slower, more memory |
| Usable as dict key / set element | Yes (if contents are hashable) | No |
| Methods available | Only `count()`, `index()` | Many (`append`, `sort`, `remove`, etc.) |
| Use case | Fixed data, records | Data that grows/shrinks/changes |

#### Key Takeaways — Tuples

- Tuples are ordered and immutable; use them for fixed collections of data.
- A single-element tuple **requires** a trailing comma.
- Tuples support only `count()` and `index()` since they can't be modified.
- A tuple can contain mutable elements, and those elements remain mutable.
- Tuples are hashable (if contents are hashable), making them valid dictionary keys — unlike lists.

---

## 2. Sets

### 2.1 Introduction to Sets

**Definition:**
A set is an **unordered** collection of **unique** and **hashable** elements. Duplicate values are automatically removed.

**Purpose / Why it is used:**
- To store collections of unique items (e.g., unique visitor IDs, unique tags).
- To perform fast membership testing (`in` operator is O(1) on average for sets vs O(n) for lists).
- To perform mathematical set operations like union, intersection, and difference.
- To quickly remove duplicates from a collection.

**Syntax:**

```python
my_set = {1, 2, 3}
empty_set = set()      # NOT {} — that creates a dict!
```

**Detailed Explanation:**
Sets are built on a hash table internally, similar to dictionaries (but storing only keys, no values). This is why elements must be hashable — meaning immutable types like numbers, strings, and tuples (of hashable items) can be set elements, but lists, dicts, and other sets cannot.

**Example:**

```python
s = {1, 2, 3, 2, 1}
print("set:", s)

empty = set()
print("empty set:", empty, type(empty))

not_a_set = {}
print("empty braces:", type(not_a_set))
```

**Output:**

```
set: {1, 2, 3}
empty set: set() <class 'set'>
empty braces: <class 'dict'>
```

**Real-world use cases:**
- Removing duplicate entries from a list of emails or IDs.
- Checking membership quickly (e.g., checking if a username is in a "banned users" set).
- Comparing two collections of data (e.g., finding common followers between two social accounts using intersection).

> **Warning:** `{}` creates an empty **dictionary**, not an empty set. Always use `set()` for an empty set.

> **Note:** Sets do **not** preserve insertion order and do not support indexing (`s[0]` is invalid).

---

### 2.2 Basic Operations on Sets

#### Adding and Removing Elements

```python
s = {1, 2, 3}
s.add(4)
print("after add:", s)

s.update([5, 6, 7])
print("after update:", s)

s.remove(7)
print("after remove:", s)

s.discard(100)   # does NOT raise an error even if 100 is not present
print("after discard nonexistent:", s)

popped = s.pop()
print("popped:", popped, "remaining:", s)

s.clear()
print("after clear:", s)
```

**Output:**

```
after add: {1, 2, 3, 4}
after update: {1, 2, 3, 4, 5, 6, 7}
after remove: {1, 2, 3, 4, 5, 6}
after discard nonexistent: {1, 2, 3, 4, 5, 6}
popped: 1 remaining: {2, 3, 4, 5, 6}
after clear: set()
```

> **Note:** `.pop()` on a set removes an **arbitrary** element (since sets are unordered), not necessarily the "first" one in any predictable sense.

#### `.remove()` vs `.discard()`

| Method | If element is missing | Use case |
|---|---|---|
| `.remove(x)` | Raises `KeyError` | When absence is unexpected/an error |
| `.discard(x)` | Does nothing (silent) | When absence is acceptable |

#### Important Points / Rules

- Set elements must be **hashable** (immutable-like) — no lists, dicts, or plain sets as elements.
- Sets are unordered — never rely on element order.
- Sets automatically eliminate duplicates.

#### Common Mistakes

- Using `{}` expecting an empty set (it's actually an empty dict).
- Using `.remove()` on a possibly-missing element and getting an unexpected `KeyError` — use `.discard()` instead if that's acceptable.
- Trying to index a set: `s[0]` raises `TypeError`.

#### Key Takeaways — Set Basics

- Sets store unique, hashable, unordered elements.
- `set()` creates an empty set; `{}` creates an empty dict.
- Use `.discard()` for safe removal, `.remove()` when missing elements should raise an error.

---

### 2.3 Set Operations: Union, Intersection, Difference

**Purpose:** Sets support mathematical set algebra, which is extremely useful for comparing collections of data.

**Syntax / Operators:**

| Operation | Operator | Method | Meaning |
|---|---|---|---|
| Union | `\|` | `.union()` | All elements from both sets |
| Intersection | `&` | `.intersection()` | Elements common to both sets |
| Difference | `-` | `.difference()` | Elements in first set but not second |
| Symmetric Difference | `^` | `.symmetric_difference()` | Elements in either set, but not both |

**Example:**

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

print("union:", A | B)
print("intersection:", A & B)
print("difference A-B:", A - B)
print("difference B-A:", B - A)
print("symmetric_difference:", A ^ B)
```

**Output:**

```
union: {1, 2, 3, 4, 5, 6}
intersection: {3, 4}
difference A-B: {1, 2}
difference B-A: {5, 6}
symmetric_difference: {1, 2, 5, 6}
```

> **Note:** `A - B` and `B - A` are **not the same** — difference is order-sensitive, unlike union and intersection.

#### Subset, Superset, and Disjoint Checks

```python
A = {1, 2, 3, 4}
C = {1, 2}

print("C subset A:", C.issubset(A))
print("A superset C:", A.issuperset(C))
print("disjoint:", A.isdisjoint({100, 200}))
```

**Output:**

```
C subset A: True
A superset C: True
disjoint: True
```

**Real-world use cases:**
- **Union:** Combining tags from two articles into one unique tag list.
- **Intersection:** Finding mutual friends between two users.
- **Difference:** Finding which items in a shopping cart are not in the "in stock" set.
- **Symmetric Difference:** Finding items that changed (added or removed) between two versions of a dataset.

#### Key Takeaways — Set Operations

- `|` = union, `&` = intersection, `-` = difference, `^` = symmetric difference.
- Difference is direction-sensitive: `A - B ≠ B - A` in general.
- `issubset()`, `issuperset()`, and `isdisjoint()` let you compare set relationships without creating new sets.

---

### 2.4 Frozenset

**Definition:**
A `frozenset` is an **immutable** version of a set. Once created, elements cannot be added or removed.

**Purpose / Why it is used:**
- To create a set that can itself be used as a dictionary key or as an element inside another set (since regular sets are unhashable and cannot be nested inside sets or used as dict keys).
- To guarantee a collection of unique values won't be accidentally modified.

**Syntax:**

```python
fs = frozenset([1, 2, 3])
```

**Example:**

```python
fs = frozenset([1, 2, 3])
print("frozenset:", fs)

try:
    fs.add(4)
except AttributeError as e:
    print("Error:", e)

fs2 = frozenset([2, 3, 4])
print("frozen union:", fs | fs2)
```

**Output:**

```
frozenset: frozenset({1, 2, 3})
Error: 'frozenset' object has no attribute 'add'
frozen union: frozenset({1, 2, 3, 4})
```

> **Note:** `frozenset` still supports **read-only** set operations like union, intersection, and difference — those return **new** frozensets rather than modifying in place.

#### Why Regular Sets Cannot Be Nested Inside Sets

```python
try:
    weird = {1, {2, 3}}
except TypeError as e:
    print("Error:", e)

nested_ok = {1, frozenset([2, 3])}
print("nested ok:", nested_ok)
```

**Output:**

```
Error: unhashable type: 'set'
nested ok: {1, frozenset({2, 3})}
```

This works because `frozenset` is hashable, but a regular `set` is not (since its contents could change, its hash would become unstable).

#### Comparison: Set vs Frozenset

| Feature | `set` | `frozenset` |
|---|---|---|
| Mutable | Yes | No |
| Hashable | No | Yes |
| Can be dict key | No | Yes |
| Can be element of another set | No | Yes |
| Methods | `add`, `remove`, `update`, etc. | Only read-only ops (`union`, `intersection`, etc.) |

#### Key Takeaways — Frozenset

- `frozenset` is the immutable, hashable counterpart to `set`.
- Use it when you need a set-like collection as a dictionary key or as an element in another set.
- All set algebra operations (union, intersection, etc.) work on frozensets and return new frozensets.

---

## 3. Dictionaries

### 3.1 Introduction to Dictionaries

**Definition:**
A dictionary (`dict`) is an unordered (technically insertion-ordered since Python 3.7+) collection of **key-value pairs**, where each key is unique and maps to a value.

**Purpose / Why it is used:**
- To store data that is naturally structured as a mapping — e.g., a name mapped to an age, a product ID mapped to its price.
- To provide very fast (average O(1)) lookup, insertion, and deletion by key.
- To represent structured/semi-structured data (similar to JSON objects).

**Syntax:**

```python
person = {"name": "Saurabh", "age": 30, "city": "Pune"}
empty_dict = {}
```

**Detailed Explanation:**
Internally, a dictionary is a hash table where each key is hashed to determine where its value is stored. This is why keys must be hashable (immutable-like), while values can be **anything**, including other dictionaries, lists, or functions.

Since Python 3.7, dictionaries **maintain insertion order** as a language guarantee (this was an implementation detail in 3.6 and became official in 3.7).

**Example:**

```python
d = {"name": "Saurabh", "age": 30, "city": "Pune"}
print(d)
print(d["name"])
print(d.get("name"))
print(d.get("country", "Not Found"))
```

**Output:**

```
{'name': 'Saurabh', 'age': 30, 'city': 'Pune'}
Saurabh
Saurabh
Not Found
```

> **Tip:** Use `.get(key, default)` instead of `d[key]` when a key might not exist — it avoids a `KeyError` and lets you supply a fallback value.

**Real-world use cases:**
- Representing a JSON API response as native Python data.
- Counting frequency of items (e.g., word counts).
- Caching/memoization: mapping function inputs to previously computed outputs.
- Configuration settings stored as key-value pairs.

#### Key Takeaways — Dictionary Introduction

- Dictionaries map unique, hashable keys to values of any type.
- `d[key]` raises `KeyError` if the key is missing; `d.get(key, default)` does not.
- Since Python 3.7, insertion order is preserved and guaranteed.

---

### 3.2 Operations on Dictionaries: Updating, Deleting, and Others

#### Adding and Updating Values

```python
d = {"name": "Saurabh", "age": 30, "city": "Pune"}

d["age"] = 31                              # update existing key
print("after update:", d)

d.update({"country": "India", "age": 32})  # update multiple keys at once
print("after .update():", d)

d["email"] = "test@example.com"            # add a new key
print("after adding key:", d)
```

**Output:**

```
after update: {'name': 'Saurabh', 'age': 31, 'city': 'Pune'}
after .update(): {'name': 'Saurabh', 'age': 32, 'city': 'Pune', 'country': 'India'}
after adding key: {'name': 'Saurabh', 'age': 32, 'city': 'Pune', 'country': 'India', 'email': 'test@example.com'}
```

#### Deleting Keys

```python
del d["email"]
print("after del:", d)

popped_val = d.pop("city")
print("popped value:", popped_val, "dict now:", d)

last_item = d.popitem()
print("popitem:", last_item, "dict now:", d)

d.clear()
print("after clear:", d)
```

**Output:**

```
after del: {'name': 'Saurabh', 'age': 32, 'country': 'India'}
popped value: Pune dict now: {'name': 'Saurabh', 'age': 32, 'country': 'India'}
popitem: ('country', 'India') dict now: {'name': 'Saurabh', 'age': 32}
after clear: {}
```

#### Dictionary Deletion / Removal Methods Compared

| Method | Behavior | Returns | Raises error if missing? |
|---|---|---|---|
| `del d[key]` | Removes key | Nothing | Yes (`KeyError`) |
| `d.pop(key)` | Removes key | The value | Yes, unless a default is given: `d.pop(key, default)` |
| `d.pop(key, default)` | Removes key | The value, or `default` | No |
| `d.popitem()` | Removes **last inserted** pair (Python 3.7+) | `(key, value)` tuple | Yes, if dict is empty |
| `d.clear()` | Removes all items | `None` | No |

#### `setdefault()`

```python
d2 = {"a": 1}
d2.setdefault("a", 100)   # key exists, value stays the same
d2.setdefault("b", 2)     # key doesn't exist, gets added
print("setdefault:", d2)
```

**Output:**

```
setdefault: {'a': 1, 'b': 2}
```

> **Tip:** `setdefault()` is useful for building dictionaries of lists, e.g., grouping items by category, without checking `if key in d` manually every time.

#### Merging Dictionaries (Python 3.9+)

```python
m1 = {"a": 1, "b": 2}
m2 = {"b": 3, "c": 4}
print(m1 | m2)   # merge operator; m2's values win on key conflicts
```

**Output:**

```
{'a': 1, 'b': 3, 'c': 4}
```

#### Dictionary Comprehension

```python
squares = {x: x**2 for x in range(5)}
print(squares)
```

**Output:**

```
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

#### Common Mistakes

- Using `d[key]` for a possibly-missing key instead of `.get()` and crashing with `KeyError`.
- Confusing `.pop()` (dict, removes by key, returns value) with list's `.pop()` (removes by index).
- Forgetting that `d.update(other_dict)` overwrites existing keys with the new dictionary's values.

#### Best Practices

- Use `.get()` when a missing key is a normal, expected situation.
- Use `.setdefault()` or `collections.defaultdict` when grouping/accumulating data.
- Use dictionary comprehensions for concise, readable transformations instead of manual loops when the logic is simple.

#### Key Takeaways — Dictionary Operations

- `d[key] = value` adds or updates; `del`, `.pop()`, `.popitem()`, and `.clear()` remove.
- `.pop(key, default)` is the safe way to remove a key without risking `KeyError`.
- `.setdefault()` avoids repetitive existence checks.
- The `|` operator (Python 3.9+) merges two dictionaries into a new one.

---

### 3.3 Working with Keys and Values in Depth

**Purpose:** To iterate over, inspect, or transform dictionary contents, Python provides three "view" objects: `.keys()`, `.values()`, and `.items()`.

**Example:**

```python
d3 = {"x": 1, "y": 2, "z": 3}

print("keys:", d3.keys(), type(d3.keys()))
print("values:", d3.values(), type(d3.values()))
print("items:", d3.items(), type(d3.items()))

for k, v in d3.items():
    print(k, "->", v)

print("k in d3:", "x" in d3)
print("v in d3.values():", 1 in d3.values())
```

**Output:**

```
keys: dict_keys(['x', 'y', 'z']) <class 'dict_keys'>
values: dict_values([1, 2, 3]) <class 'dict_values'>
items: dict_items([('x', 1), ('y', 2), ('z', 3)]) <class 'dict_items'>
x -> 1
y -> 2
z -> 3
k in d3: True
v in d3.values(): True
```

#### Understanding View Objects

| View | Returns | Notes |
|---|---|---|
| `d.keys()` | `dict_keys` — a view of all keys | Dynamic — reflects live changes to `d` |
| `d.values()` | `dict_values` — a view of all values | Dynamic; may contain duplicates |
| `d.items()` | `dict_items` — a view of `(key, value)` tuples | Most commonly used for iteration |

> **Note:** `.keys()`, `.values()`, and `.items()` return **view objects**, not lists. They dynamically reflect changes to the dictionary. Convert with `list(d.keys())` if you need a static snapshot.

```python
d4 = {"a": 1}
keys_view = d4.keys()
d4["b"] = 2
print(list(keys_view))   # reflects the new key automatically
```

**Output:**

```
['a', 'b']
```

#### Membership Testing: Keys vs Values

- `key in d` checks the **keys** — this is fast (O(1) average), because it uses the hash table directly.
- `value in d.values()` checks the **values** — this is slower (O(n)), because it has to scan every value linearly.

> **Tip:** Default membership testing (`x in d`) checks keys, not values. If you need to check for a value, use `x in d.values()` explicitly, and be aware it's less efficient for large dictionaries.

#### What Data Types Apply to Keys and Values

| Element | Allowed Types | Restriction |
|---|---|---|
| **Key** | `int`, `float`, `str`, `bool`, `tuple` (of hashable items), `frozenset` | Must be **hashable** (effectively, immutable) |
| **Value** | Anything — `int`, `str`, `list`, `dict`, `tuple`, `set`, functions, objects, even other dictionaries | No restriction |

**Example — mixed value types:**

```python
mixed_vals = {
    "list": [1, 2, 3],
    "dict": {"nested": True},
    "tuple": (1, 2),
    "func": print
}
print(mixed_vals["list"], mixed_vals["dict"], mixed_vals["tuple"])
```

**Output:**

```
[1, 2, 3] {'nested': True} (1, 2)
```

#### Key Takeaways — Keys and Values

- `.keys()`, `.values()`, `.items()` return dynamic **view objects**, not static lists.
- Checking `x in d` tests keys (fast); checking `x in d.values()` tests values (slower, linear scan).
- Keys must be hashable; values can be of any type, including nested dictionaries or lists.

---

### 3.4 Allowed and Not Allowed Types of Keys and Values

**Core Rule:** A dictionary key must be **hashable**. An object is hashable if its hash value never changes during its lifetime, which in practice means it must be **immutable** (or behave immutably from a hashing perspective).

#### Allowed Key Types

```python
valid_keys = {
    1: "int key",
    "a": "str key",
    (1, 2): "tuple key",
    True: "bool key",
    3.14: "float key"
}
print(valid_keys)
```

**Output:**

```
{1: 'bool key', 'a': 'str key', (1, 2): 'tuple key', 3.14: 'float key'}
```

> **Warning:** Notice that the key `1` disappeared and was overwritten by `True`! This is because in Python, `True == 1` and `hash(True) == hash(1)`. When you use both `1` and `True` as dictionary keys, they collide — the **later** assignment wins. This is a subtle and common source of bugs.

#### Not Allowed Key Types

```python
try:
    bad = {[1, 2]: "list key"}
except TypeError as e:
    print("Error list key:", e)

try:
    bad2 = {{1, 2}: "set key"}
except TypeError as e:
    print("Error set key:", e)

try:
    bad3 = {{"a": 1}: "dict key"}
except TypeError as e:
    print("Error dict key:", e)
```

**Output:**

```
Error list key: unhashable type: 'list'
Error set key: unhashable type: 'set'
Error dict key: unhashable type: 'dict'
```

#### Summary Table — Key and Value Type Rules

| Type | Valid as Key? | Valid as Value? | Reason |
|---|---|---|---|
| `int` | Yes | Yes | Immutable, hashable |
| `float` | Yes | Yes | Immutable, hashable |
| `str` | Yes | Yes | Immutable, hashable |
| `bool` | Yes | Yes | Immutable; note `True`/`False` collide with `1`/`0` |
| `tuple` (all elements hashable) | Yes | Yes | Immutable, hashable if contents are too |
| `frozenset` | Yes | Yes | Immutable, hashable |
| `list` | **No** | Yes | Mutable, unhashable |
| `set` | **No** | Yes | Mutable, unhashable |
| `dict` | **No** | Yes | Mutable, unhashable |
| Custom object (default) | Yes | Yes | Hashable by default (based on `id()`) unless `__eq__` is overridden without `__hash__` |

> **Note:** A tuple is only usable as a key if **every element inside it** is also hashable. `(1, [2, 3])` is **not** a valid key because it contains a list.

#### Common Mistakes

- Trying to use a list as a dictionary key (very common when trying to use coordinates like `[x, y]` — use a tuple `(x, y)` instead).
- Not realizing `True`/`1` and `False`/`0` collide as dictionary keys.
- Assuming values have type restrictions like keys do — they don't.

#### Best Practices

- Use tuples instead of lists for composite/multi-part keys.
- Be explicit with boolean vs integer keys to avoid accidental key collisions.
- When you need a "set" as a key, convert it to a `frozenset` first.

#### Key Takeaways — Key/Value Type Rules

- Dictionary **keys must be hashable** (effectively immutable); **values have no type restriction**.
- Lists, sets, and dicts cannot be used as keys because they are mutable and therefore unhashable.
- `True` and `1` (and `False` and `0`) are treated as equal keys — this can silently overwrite data.

---

## 4. Mutability and Immutability

### 4.1 Core Concept

**Definition:**
- A **mutable** object can be changed in place after creation — its identity (`id()`) stays the same, but its internal state/content can change.
- An **immutable** object cannot be changed after creation — any "modification" actually creates a **new object** in memory.

**Purpose / Why it matters:**
Understanding mutability is essential for:
- Predicting whether a function can modify data passed into it.
- Avoiding unexpected side effects when objects are shared between variables.
- Understanding what can and cannot be used as dictionary keys or set elements.
- Knowing when you need to copy data versus when you can safely share references.

| Category | Examples |
|---|---|
| **Mutable** | `list`, `dict`, `set`, custom classes (by default) |
| **Immutable** | `int`, `float`, `str`, `tuple`, `bool`, `frozenset`, `bytes` |

---

### 4.2 Mutability in Lists

```python
lst = [1, 2, 3]
print("id before:", id(lst))
lst.append(4)
print("id after append:", id(lst), lst)
```

**Output:**

```
id before: 140361105478336
id after append: 140361105478336 [1, 2, 3, 4]
```

> **Note:** The `id()` (memory address) stays **the same** before and after `.append()`. The list object itself was modified in place — no new object was created.

---

### 4.3 Immutability in Tuples

```python
t = (1, 2, 3)
try:
    t[0] = 100
except TypeError as e:
    print("Error mutating tuple:", e)
```

**Output:**

```
Error mutating tuple: 'tuple' object does not support item assignment
```

Tuples simply do not provide any operation that changes their contents — there is no `.append()`, `.remove()`, or item assignment support.

---

### 4.4 Immutability in Strings

```python
s = "hello"
print("id before:", id(s))
s2 = s + " world"
print("id after concat (new object):", id(s2), s2)
print("original s unchanged:", s)
```

**Output:**

```
id before: 140361100963696
id after concat (new object): 140361101180336 hello world
original s unchanged: hello
```

Notice that `s + " world"` did **not** modify `s` — it created a brand-new string object `s2` with a **different** `id()`. The original string `s` remains completely unchanged. This is true for every string "modification" method (`.upper()`, `.replace()`, `.strip()`, etc.) — they all return new strings.

#### Comparison: Mutable vs Immutable Behavior

| Aspect | Mutable (e.g., `list`) | Immutable (e.g., `tuple`, `str`) |
|---|---|---|
| In-place modification | Yes | No |
| `id()` after "modification" | Same | Changes (new object created) |
| Can be a dict key / set element | No | Yes (if contents are hashable) |
| Thread-safety by default | Lower (shared state can change) | Higher (value never changes) |
| Passing to functions | Function can modify the caller's object | Function cannot alter the original |

---

### 4.5 The Special Case: Mutable Objects Inside Immutable Containers

A tuple is immutable, but that only means the tuple **itself** cannot add, remove, or reassign its elements. If one of its elements is a mutable object (like a list), **that inner object can still be modified**.

```python
t2 = ([1, 2], 3)
t2[0].append(99)
print("tuple with mutable inner list:", t2)
```

**Output:**

```
tuple with mutable inner list: ([1, 2, 99], 3)
```

> **Warning:** This is a very common point of confusion. `t2[0] = [5, 6]` would fail (you can't reassign what index 0 points to), but `t2[0].append(99)` succeeds (you're mutating the object that index 0 already points to, not changing what it points to).

#### Key Takeaways — Mutability and Immutability

- Mutable objects (`list`, `dict`, `set`) can change in place; their `id()` stays constant.
- Immutable objects (`tuple`, `str`, `int`, `frozenset`) cannot change in place; any "change" produces a new object.
- A tuple can hold mutable elements, and those elements remain independently mutable — immutability applies only to the tuple's own structure, not to what its elements contain.
- Only immutable (hashable) types can be used as dictionary keys or set elements.

---

## 5. Shallow Copy vs Deep Copy — Deep Walkthrough

**Definition:**
- A **shallow copy** creates a new outer object, but the elements inside it are still **references to the same inner objects** as the original.
- A **deep copy** recursively creates brand-new copies of the outer object **and every nested object inside it**, so nothing is shared with the original.

**Purpose / Why it matters:**
When your data contains nested mutable structures (lists inside lists, dicts inside dicts, etc.), a simple copy might not fully "detach" the copy from the original. Understanding this prevents a very common class of bugs where modifying a "copy" unexpectedly changes the original.

**Syntax:**

```python
import copy

shallow = original.copy()        # or list(original), or original[:]
deep = copy.deepcopy(original)
```

### Step-by-Step Walkthrough

#### Step 1: Shallow Copy — Top-Level Change

```python
original = [1, [2, 3], {"a": 4}]
shallow = original.copy()

shallow[0] = 100
print("after changing top-level in shallow:", original, shallow)
```

**Output:**

```
after changing top-level in shallow: [1, [2, 3], {'a': 4}] [100, [2, 3], {'a': 4}]
```

At the **top level**, changing `shallow[0]` did **not** affect `original`. This is because index `0` held an immutable `int` (`1`), and reassigning `shallow[0]` just made `shallow`'s slot point to a new value (`100`) — it did not touch `original`'s slot at all.

#### Step 2: Shallow Copy — Nested Mutation (The Gotcha)

```python
shallow[1].append(999)
print("after mutating nested list via shallow:", original, shallow)
```

**Output:**

```
after mutating nested list via shallow: [1, [2, 3, 999], {'a': 4}] [100, [2, 3, 999], {'a': 4}]
```

This time, **both** `original` and `shallow` changed! Why? Because `.copy()` only copies the **outer** list. The inner list at index `1` is the **same object** in both `original` and `shallow` — `shallow` just holds a reference to it, not an independent copy.

```python
print("original[1] is shallow[1]:", original[1] is shallow[1])
```

**Output:**

```
original[1] is shallow[1]: True
```

The `is` check confirms it: they are literally the same object in memory.

#### Step 3: Deep Copy — Full Independence

```python
import copy

deep = copy.deepcopy(original)
deep[1].append(12345)
print("after mutating nested list via deepcopy:", original, deep)
print("original[1] is deep[1]:", original[1] is deep[1])
```

**Output:**

```
after mutating nested list via deepcopy: [1, [2, 3, 999], {'a': 4}] [1, [2, 3, 999, 12345], {'a': 4}]
original[1] is deep[1]: False
```

With `copy.deepcopy()`, the inner list was **recursively copied** too. Modifying `deep[1]` had **zero effect** on `original`. The `is` check confirms they are now completely separate objects.

#### Step 4: Other Ways to Create a Shallow Copy

Slicing and `copy.copy()` behave the same as `.copy()` — all of them are shallow:

```python
lst_a = [[1], [2]]
lst_b = lst_a[:]          # slice copy — still shallow
lst_b[0].append(9)
print("slice shallow copy:", lst_a, lst_b)
```

**Output:**

```
slice shallow copy: [[1, 9], [2]] [[1, 9], [2]]
```

#### Step 5: Strings — Why Copying Isn't a Concern

Since strings are immutable, there's no shallow/deep distinction to worry about — any "modification" always produces a brand-new string, so there's never a shared mutable reference to accidentally affect.

```python
str_a = "abc"
str_b = str_a
str_b += "d"
print(str_a, str_b)
```

**Output:**

```
abc abcd
```

`str_b += "d"` created a new string object and rebound `str_b` to it; `str_a` was never touched.

### Visual Summary of the Difference

| Action | Original List | Copy Method | Nested list shared? |
|---|---|---|---|
| `shallow = original.copy()` | `[1, [2,3], {"a":4}]` | Shallow | **Yes** — same inner list object |
| `shallow = original[:]` | `[1, [2,3], {"a":4}]` | Shallow | **Yes** — same inner list object |
| `shallow = copy.copy(original)` | `[1, [2,3], {"a":4}]` | Shallow | **Yes** — same inner list object |
| `deep = copy.deepcopy(original)` | `[1, [2,3], {"a":4}]` | Deep | **No** — independent copy |
| `x = original` (no copy at all) | `[1, [2,3], {"a":4}]` | Not a copy — same object | Everything is shared |

### When to Use Which

| Situation | Recommended Approach |
|---|---|
| Data is flat (no nested lists/dicts) | Shallow copy (`.copy()`, slicing) is sufficient |
| Data has nested mutable structures and you need full independence | Deep copy (`copy.deepcopy()`) |
| You want two variables to always reflect the same underlying data (shared state intentionally) | Don't copy at all — just assign (`b = a`) |
| Performance matters and structure is simple | Shallow copy (deep copy is slower — it recursively processes everything) |

#### Common Mistakes

- Assuming `.copy()` fully isolates nested data — it only isolates the top level.
- Using `x = original` and thinking it's a copy — it's actually just another name for the same object (no copy at all).
- Using `copy.deepcopy()` unnecessarily on flat/simple structures, adding avoidable performance overhead.

#### Best Practices

- Use `is` to check whether two variables reference the exact same object when debugging copy-related bugs.
- Default to shallow copies for simple, flat data; reach for `deepcopy()` only when nested mutable structures are involved.
- Be especially careful with default mutable arguments in function definitions (a related and very common Python pitfall), since they behave like shared references across calls.

> **Tip:** A quick mental model: shallow copy duplicates the "box," but the "items" inside can still be shared. Deep copy duplicates the box **and** everything inside it, all the way down.

#### Key Takeaways — Shallow vs Deep Copy

- Shallow copy duplicates only the outer/top-level container; nested mutable objects remain shared with the original.
- Deep copy recursively duplicates every level, producing a fully independent structure.
- Use `original.copy()`, `list(original)`, or `original[:]` for shallow copies; use `copy.deepcopy()` for deep copies.
- Immutable objects (like strings) never need this distinction, since they can't be mutated in place at all.
- Use the `is` operator to verify whether two references point to the same underlying object.

---

## 6. Summary

This guide walked through four interconnected areas of Python's core data model:

- **Tuples** are ordered, immutable sequences — ideal for fixed data and usable as dictionary keys.
- **Sets** store unique, hashable, unordered elements and support powerful set algebra (union, intersection, difference, symmetric difference); **frozenset** provides an immutable, hashable version.
- **Dictionaries** map hashable keys to values of any type, with rich tools for updating, deleting, and inspecting data via `.keys()`, `.values()`, and `.items()`.
- **Mutability** determines whether an object can change in place (`list`, `dict`, `set`) or must be replaced entirely to "change" (`tuple`, `str`, `int`, `frozenset`).
- **Shallow vs deep copying** matters specifically because of mutability — shallow copies share nested mutable objects with the original, while deep copies fully detach every level of nested structure.

The unifying thread across all these topics is **hashability and mutability**: they determine what can be a dictionary key, what can be a set element, what a function can silently modify, and what a "copy" actually protects you from.

---

## 7. Quick Revision / Cheat Sheet

**Tuples**
```python
t = (1, 2, 3)          # create
t[0]                    # access
t.count(x); t.index(x)  # only 2 methods
t[0] = 5                # ERROR — immutable
```

**Sets**
```python
s = {1, 2, 3}
s.add(x); s.update([..]); s.remove(x); s.discard(x); s.pop()
A | B   # union
A & B   # intersection
A - B   # difference
A ^ B   # symmetric difference
frozenset([1,2,3])   # immutable set
```

**Dictionaries**
```python
d = {"key": "value"}
d[key]; d.get(key, default)
d[key] = value           # add/update
del d[key]; d.pop(key); d.popitem(); d.clear()
d.keys(); d.values(); d.items()
d1 | d2                  # merge (3.9+)
```

**Mutability**
```python
list  -> mutable   (id stays same on modification)
tuple -> immutable (id changes; new object on "change")
str   -> immutable
dict  -> mutable
set   -> mutable
frozenset -> immutable
```

**Copying**
```python
shallow = original.copy()      # or original[:], copy.copy(original)
deep = copy.deepcopy(original)
a is b   # True only if same object in memory
```

| Type | Ordered? | Mutable? | Hashable? | Allows Duplicates? |
|---|---|---|---|---|
| `list` | Yes | Yes | No | Yes |
| `tuple` | Yes | No | Yes* | Yes |
| `set` | No | Yes | No | No |
| `frozenset` | No | No | Yes | No |
| `dict` (keys) | Yes (insertion) | Keys: No, Values: Yes | Keys: Yes | Keys: No, Values: Yes |

*\*Tuple is hashable only if all its elements are hashable.*

---

## 8. Common Interview Questions

1. **What is the difference between a list and a tuple?**
   A list is mutable and defined with `[]`; a tuple is immutable and defined with `()`. Tuples are hashable (if their contents are) and can be used as dictionary keys, while lists cannot.

2. **Why can't a list be used as a dictionary key?**
   Because dictionary keys must be hashable, and hashability requires immutability. Lists are mutable, so their hash value could change over time, which would break the dictionary's internal hash table.

3. **What is the difference between `.remove()` and `.discard()` on a set?**
   `.remove()` raises a `KeyError` if the element doesn't exist; `.discard()` does nothing silently in that case.

4. **What is a frozenset and when would you use it?**
   A `frozenset` is an immutable, hashable version of a set. Use it when you need a set-like collection to be a dictionary key or an element of another set.

5. **What's the difference between `d.get(key)` and `d[key]`?**
   `d[key]` raises `KeyError` if the key doesn't exist; `d.get(key, default)` returns `None` (or a specified default) instead of raising an error.

6. **Why do `1` and `True` collide as dictionary keys?**
   Because `True == 1` and `hash(True) == hash(1)` in Python — booleans are a subtype of integers, so they hash identically and are treated as the same key.

7. **What is the difference between shallow copy and deep copy?**
   A shallow copy duplicates only the outer container; nested mutable objects remain shared references with the original. A deep copy recursively duplicates every nested level, producing a fully independent object graph.

8. **Can a tuple contain mutable elements? Does that violate immutability?**
   Yes, a tuple can contain a list. This doesn't violate immutability — the tuple itself still can't be resized or have its element references reassigned, but the mutable object it references can still be changed internally.

9. **What is the time complexity of membership testing (`in`) in a list vs a set?**
   O(n) for a list (linear scan) vs O(1) average for a set (hash table lookup).

10. **What happens if you use `x = original_list` instead of copying it?**
    No copy is made at all — `x` and `original_list` refer to the exact same object in memory. Modifying one through a mutating method affects the other.

---

## 9. Practice Exercises

1. Create a tuple of 5 different fruit names. Try to change the second element and observe the error.
2. Write a function that accepts two lists and returns their common elements using sets (intersection).
3. Given `{1, 2, 3}` and `{2, 3, 4}`, compute and print the union, intersection, difference (both directions), and symmetric difference.
4. Create a `frozenset` from a list of numbers, then try to add an element to it and handle the resulting error gracefully.
5. Build a dictionary representing a student (`name`, `age`, `grades` as a list). Add a new key, update an existing value, and delete one key.
6. Write code that demonstrates why `True` and `1` cannot both exist as separate dictionary keys.
7. Create a nested list `data = [[1, 2], [3, 4]]`. Make a shallow copy and a deep copy. Modify the first inner list in each copy and observe which one affects `data`.
8. Explain (in your own words, then verify with code) why `t = (1, [2, 3])` is not fully immutable.
9. Write a dictionary comprehension that maps each word in a sentence to its length.
10. Given a list with duplicate values, use a set to remove duplicates while preserving the ability to still access the original list afterward.

> **Tip:** For each exercise, try predicting the output *before* running the code — this is one of the most effective ways to solidify your understanding of mutability, hashing, and copying behavior.
