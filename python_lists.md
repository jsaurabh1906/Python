# Python Lists — Complete Reference Guide

## Overview

Lists are one of Python's most versatile and widely used built-in data structures. They allow you to store an ordered, changeable collection of items — of any data type, mixed together if needed — in a single variable.

This document is a complete, structured reference covering Python lists in depth, organized into four main areas:

1. **Introduction to Lists** — what lists are, how to create them, and their core characteristics.
2. **List Operations** — slicing, concatenation, repetition, and the full set of built-in list methods (`append`, `insert`, `extend`, `remove`, `pop`, `reverse`, `sort`, `count`, membership testing).
3. **Numerical Operations on List Elements** — performing calculations (sum, min, max, average) on numbers stored in lists.
4. **Nested Lists** — lists that contain other lists, including 2D grid/matrix-style structures.

Each topic includes definitions, syntax, detailed explanations, verified examples with output, real-world use cases, common mistakes, and best practices — making this document useful both for first-time learning and for later reference.

> **Note:** All examples in this document use Python 3 syntax and have been verified to run correctly.

---

## Table of Contents

1. [Introduction to Lists](#introduction-to-lists)
   - [What Is a List?](#what-is-a-list)
   - [Creating Lists](#creating-lists)
   - [List Characteristics](#list-characteristics)
   - [Accessing List Elements](#accessing-list-elements)
   - [Lists vs Other Data Types](#lists-vs-other-data-types)
2. [List Operations](#list-operations)
   - [Slicing Lists](#slicing-lists)
   - [Concatenation](#concatenation)
   - [Repetition](#repetition)
   - [`append()`](#append)
   - [`insert()`](#insert)
   - [`extend()`](#extend)
   - [`remove()`](#remove)
   - [`pop()`](#pop)
   - [`reverse()`](#reverse)
   - [`sort()`](#sort)
   - [`count()`](#count)
   - [Membership Testing (`in`, `not in`)](#membership-testing-in-not-in)
   - [Other Useful List Methods](#other-useful-list-methods)
3. [Numerical Operations on List Elements](#numerical-operations-on-list-elements)
   - [`sum()`, `min()`, `max()`](#sum-min-max)
   - [Calculating Average](#calculating-average)
   - [List Comprehensions for Numerical Transformations](#list-comprehensions-for-numerical-transformations)
   - [Using `map()` for Numerical Operations](#using-map-for-numerical-operations)
4. [Nested Lists](#nested-lists)
   - [What Are Nested Lists?](#what-are-nested-lists)
   - [Accessing Elements in Nested Lists](#accessing-elements-in-nested-lists)
   - [Modifying Nested Lists](#modifying-nested-lists)
   - [Iterating Through Nested Lists](#iterating-through-nested-lists)
   - [Nested Lists as Matrices](#nested-lists-as-matrices)
   - [Shallow Copy vs Deep Copy in Nested Lists](#shallow-copy-vs-deep-copy-in-nested-lists)
5. [Other Related Topics](#other-related-topics)
   - [List Comprehensions](#list-comprehensions)
   - [Copying Lists](#copying-lists)
   - [`len()` and Common Built-in Functions](#len-and-common-built-in-functions)
6. [Overall Summary](#overall-summary)
7. [Quick Revision / Cheat Sheet](#quick-revision--cheat-sheet)
8. [Common Interview Questions](#common-interview-questions)
9. [Practice Exercises](#practice-exercises)

---

## Introduction to Lists

### What Is a List?

A **list** is a built-in Python data structure used to store an **ordered**, **mutable** (changeable) collection of items. Lists are defined using square brackets `[]`, with items separated by commas.

```python
fruits = ["apple", "banana", "cherry"]
print(fruits)
```

**Output:**
```
['apple', 'banana', 'cherry']
```

### Purpose / Why Lists Are Used

- To store multiple related values in a single variable instead of creating separate variables for each.
- To maintain the **order** in which items were added.
- To allow **modification** — adding, removing, or changing items after creation.
- To store **mixed data types** together, or homogeneous data like a series of numbers.

### Creating Lists

```python
# Empty list
empty_list = []
also_empty = list()

# List of strings
names = ["Saurabh", "Priya", "Aman"]

# List of numbers
numbers = [10, 20, 30, 40]

# Mixed data types
mixed = ["Saurabh", 28, 5.9, True]

# Using the list() constructor
from_string = list("Python")   # Converts an iterable into a list
from_range = list(range(5))

print(names)
print(numbers)
print(mixed)
print(from_string)
print(from_range)
```

**Output:**
```
['Saurabh', 'Priya', 'Aman']
[10, 20, 30, 40]
['Saurabh', 28, 5.9, True]
['P', 'y', 't', 'h', 'o', 'n']
[0, 1, 2, 3, 4]
```

**Explanation:** `list()` can convert any **iterable** (string, tuple, range, set, etc.) into a list. `list("Python")` breaks the string into individual characters because strings are iterable character-by-character.

### List Characteristics

| Characteristic | Description |
|-----------------|-------------|
| **Ordered** | Items maintain the position/order in which they were inserted. |
| **Mutable** | Items can be changed, added, or removed after creation. |
| **Indexed** | Each item has a numeric index, starting at `0`. |
| **Allows duplicates** | The same value can appear multiple times. |
| **Allows mixed types** | A single list can hold strings, numbers, booleans, other lists, etc. |
| **Dynamic size** | Lists grow and shrink automatically as items are added/removed. |

### Accessing List Elements

Lists use zero-based indexing, just like strings.

```python
fruits = ["apple", "banana", "cherry", "date"]

print(fruits[0])      # First element
print(fruits[2])      # Third element
print(fruits[-1])     # Last element
print(fruits[-2])     # Second-to-last element
```

**Output:**
```
apple
cherry
date
cherry
```

**Explanation:** Positive indices count from the start (beginning at `0`); negative indices count from the end (beginning at `-1`).

> **Warning:** Accessing an index that doesn't exist raises an `IndexError`. For example, `fruits[10]` on a 4-item list will crash the program. Always validate index ranges, especially with dynamic or user-supplied data.

```python
fruits = ["apple", "banana"]
# print(fruits[5])   # This would raise: IndexError: list index out of range
```

### Modifying Elements

Since lists are mutable, you can directly change an element by assigning to its index.

```python
fruits = ["apple", "banana", "cherry"]
fruits[1] = "blueberry"
print(fruits)
```

**Output:**
```
['apple', 'blueberry', 'cherry']
```

### Lists vs Other Data Types

| Feature | List `[]` | Tuple `()` | Set `{}` | Dictionary `{key: value}` |
|---------|-----------|------------|----------|-----------------------------|
| Ordered | Yes | Yes | No (unordered) | Yes (insertion order, 3.7+) |
| Mutable | Yes | No | Yes | Yes |
| Allows duplicates | Yes | Yes | No | Keys: No, Values: Yes |
| Indexed access | Yes | Yes | No | By key, not index |
| Syntax | `[1, 2, 3]` | `(1, 2, 3)` | `{1, 2, 3}` | `{"a": 1}` |
| Use case | General-purpose ordered collection | Fixed, unchangeable data | Unique items, fast membership checks | Key-value mapping |

> **Note:** Choose a **list** when you need an ordered, changeable collection. Choose a **tuple** when the data shouldn't change (e.g., coordinates). Choose a **set** when you need uniqueness and don't care about order. Choose a **dictionary** when you need to look up values by a meaningful key rather than a position.

### Key Takeaways

- A list is an ordered, mutable, indexable collection defined with `[]`.
- Lists can hold mixed data types and allow duplicate values.
- Elements are accessed via zero-based indexing; negative indices count from the end.
- Lists differ from tuples (immutable), sets (unordered, unique), and dictionaries (key-based) — pick the right structure based on whether you need order, mutability, and/or uniqueness.

---

## List Operations

### Slicing Lists

#### Definition

**Slicing** extracts a portion of a list using the syntax `list[start:stop:step]`, returning a **new list** containing the selected elements.

#### Purpose / Why It Is Used

- To extract a subset of items without modifying the original list.
- To create reversed or reordered copies.
- To split large lists into smaller chunks.

#### Syntax

```python
list[start:stop:step]
```

This works identically in concept to string slicing: `start` is inclusive, `stop` is exclusive, and `step` controls the interval and direction.

#### Examples

```python
numbers = [10, 20, 30, 40, 50, 60]

print(numbers[1:4])      # Index 1 up to (not including) 4
print(numbers[:3])       # From the start up to index 3
print(numbers[3:])       # From index 3 to the end
print(numbers[-3:])      # Last 3 elements
print(numbers[::2])      # Every 2nd element
print(numbers[::-1])     # Reversed list
```

**Output:**
```
[20, 30, 40]
[10, 20, 30]
[40, 50, 60]
[40, 50, 60]
[10, 30, 50]
[60, 50, 40, 30, 20, 10]
```

**Explanation:** `numbers[::-1]` reverses the entire list using a negative step — this is the idiomatic way to reverse a list without modifying the original (compare with `.reverse()`, covered later, which reverses **in place**).

#### Important Points / Rules

- Slicing always returns a **new list**; the original list is unaffected.
- `stop` index is exclusive, exactly like string slicing.
- Slicing never raises an `IndexError`, even with out-of-range indices — results are simply clipped.
- `list[:]` creates a shallow copy of the entire list.

```python
numbers = [10, 20, 30]
print(numbers[10:20])   # Out of range, but no error
print(numbers[:])       # Full shallow copy
```

**Output:**
```
[]
[10, 20, 30]
```

#### Modifying a List Using Slice Assignment

Unlike strings, lists are mutable, so you can assign to a slice to replace multiple elements at once.

```python
numbers = [10, 20, 30, 40, 50]
numbers[1:3] = [99, 100]
print(numbers)

# Slice assignment can also change the list's length
numbers[1:3] = [1, 2, 3, 4]
print(numbers)
```

**Output:**
```
[10, 99, 100, 40, 50]
[10, 1, 2, 3, 4, 40, 50]
```

> **Note:** This is a key difference from strings — slice assignment is **not possible** on strings (since strings are immutable) but works fine on lists.

#### Common Mistakes

```python
numbers = [10, 20, 30]

# Mistake: Expecting slicing to modify the original list
sliced = numbers[0:2]
sliced.append(999)
print(numbers)   # Original list is untouched
print(sliced)
```

**Output:**
```
[10, 20, 30]
[10, 20, 999]
```

> **Warning:** Slicing creates a new list object. Modifying the sliced result does **not** affect the original list — a very common source of confusion for beginners expecting a "view" into the original list (Python lists don't support views the way NumPy arrays do).

---

### Concatenation

#### Definition

**Concatenation** combines two or more lists into a single new list using the `+` operator.

#### Purpose / Why It Is Used

- To merge separate lists into one.
- To build a combined dataset from multiple sources.

#### Syntax

```python
new_list = list1 + list2
```

#### Examples

```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]

combined = list1 + list2
print(combined)

# Concatenating more than two lists
list3 = [7, 8]
all_combined = list1 + list2 + list3
print(all_combined)
```

**Output:**
```
[1, 2, 3, 4, 5, 6]
[1, 2, 3, 4, 5, 6, 7, 8]
```

**Explanation:** The `+` operator creates a **brand-new list** containing all elements from both lists in order; it does not modify `list1` or `list2`.

#### `+` vs `extend()`

| Aspect | `+` (Concatenation) | `extend()` |
|--------|----------------------|------------|
| Returns | A new list | `None` (modifies in place) |
| Original lists modified? | No | Yes, the list calling `extend()` is modified |
| Performance for repeated merges | Less efficient (creates new list each time) | More efficient for building up one list |

```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]

result = list1 + list2   # New list created
print(list1)              # list1 unchanged
print(result)
```

**Output:**
```
[1, 2, 3]
[1, 2, 3, 4, 5, 6]
```

#### Common Mistakes

```python
list1 = [1, 2, 3]
# Mistake: Trying to concatenate a list with a non-list directly
# combined = list1 + 4        # TypeError: can only concatenate list (not "int") to list

# Correct way to add a single item using concatenation
combined = list1 + [4]
print(combined)
```

**Output:**
```
[1, 2, 3, 4]
```

> **Warning:** The `+` operator requires **both operands to be lists**. To add a single non-list value via concatenation, you must wrap it in a list first (`[value]`), or use `.append()` instead.

---

### Repetition

#### Definition

The repetition operator `*` repeats the elements of a list a specified number of times, producing a new list.

#### Purpose / Why It Is Used

- To quickly initialize a list with repeated placeholder values.
- To generate patterns or padded structures.

#### Syntax

```python
new_list = list1 * n
```

#### Examples

```python
zeros = [0] * 5
print(zeros)

pattern = [1, 2] * 3
print(pattern)

placeholders = ["-"] * 10
print(placeholders)
```

**Output:**
```
[0, 0, 0, 0, 0]
[1, 2, 1, 2, 1, 2]
['-', '-', '-', '-', '-', '-', '-', '-', '-', '-']
```

**Explanation:** `[1, 2] * 3` repeats the entire sequence `[1, 2]` three times, not each element individually.

#### Important Points / Rules

- `list * n` where `n <= 0` returns an empty list.
- Repetition works on the whole list as a unit, not per-element.

```python
print([1, 2, 3] * 0)
print([1, 2, 3] * -1)
```

**Output:**
```
[]
[]
```

#### Common Mistakes — The Nested Mutable Object Trap

```python
# Mistake: Using repetition to create a "2D list" of mutable objects
grid = [[0] * 3] * 3
print(grid)

grid[0][0] = 99
print(grid)   # All rows change! Not what most beginners expect
```

**Output:**
```
[[0, 0, 0], [0, 0, 0], [0, 0, 0]]
[[99, 0, 0], [99, 0, 0], [99, 0, 0]]
```

> **Warning:** This is one of the most common and dangerous list mistakes in Python. `[[0] * 3] * 3` does **not** create three independent inner lists — it creates **three references to the same inner list object**. Modifying one row modifies all of them. The correct way to build a 2D grid is shown below.

```python
# Correct way: use a list comprehension to create independent rows
grid = [[0] * 3 for _ in range(3)]
grid[0][0] = 99
print(grid)
```

**Output:**
```
[[99, 0, 0], [0, 0, 0], [0, 0, 0]]
```

> **Tip:** Whenever you need a 2D structure of mutable objects (like lists), always build each row independently using a list comprehension — never use `*` repetition on a list containing a mutable inner list.

### Real-World Use Cases (Slicing, Concatenation, Repetition)

- Slicing: pagination (`items[page*10:(page+1)*10]`), extracting recent records (`data[-7:]` for the last 7 days).
- Concatenation: merging results from multiple API calls or data sources into a single list.
- Repetition: initializing a fixed-size buffer, scoreboard, or grid with default values.

---

### `append()`

#### Definition

`append()` adds a **single item** to the end of a list, modifying the list **in place**.

#### Purpose / Why It Is Used

- To add new items to a list one at a time, such as while processing data in a loop.

#### Syntax

```python
list.append(item)
```

#### Examples

```python
fruits = ["apple", "banana"]
fruits.append("cherry")
print(fruits)

# Appending a list adds it as a SINGLE nested element, not merged
fruits.append(["date", "fig"])
print(fruits)
```

**Output:**
```
['apple', 'banana', 'cherry']
['apple', 'banana', 'cherry', ['date', 'fig']]
```

**Explanation:** `append()` always adds exactly **one** element, regardless of that element's type. If you pass a list, the entire list becomes a single nested item — it is not flattened or merged in.

#### Important Points / Rules

- `append()` returns `None` — it modifies the list in place and does not return the modified list.
- Adds exactly one element per call, even if that element is itself a list, tuple, or dictionary.

#### Common Mistakes

```python
fruits = ["apple", "banana"]
fruits = fruits.append("cherry")   # Mistake: reassigning to the None return value
print(fruits)
```

**Output:**
```
None
```

> **Warning:** `append()` modifies the list in place and returns `None`. Writing `fruits = fruits.append(...)` overwrites `fruits` with `None`, silently destroying the list. Call `.append()` as a standalone statement, without reassignment.

#### Real-World Use Cases

- Building up a list of results inside a loop (e.g., collecting valid records while parsing a file).
- Adding new user entries to a list one at a time.

---

### `insert()`

#### Definition

`insert()` adds an item at a **specific index position**, shifting subsequent elements to the right.

#### Syntax

```python
list.insert(index, item)
```

#### Examples

```python
fruits = ["apple", "banana", "cherry"]
fruits.insert(1, "blueberry")
print(fruits)

# Inserting at index 0 adds to the beginning
fruits.insert(0, "avocado")
print(fruits)

# Inserting beyond the list length just appends at the end
fruits.insert(100, "zucchini")
print(fruits)
```

**Output:**
```
['apple', 'blueberry', 'banana', 'cherry']
['avocado', 'apple', 'blueberry', 'banana', 'cherry']
['avocado', 'apple', 'blueberry', 'banana', 'cherry', 'zucchini']
```

**Explanation:** If the given index is beyond the list's length, Python doesn't raise an error — it simply inserts the item at the end, behaving like `append()`.

#### Important Points / Rules

- `insert()` shifts all elements at and after the given index one position to the right.
- Negative indices are supported and count from the end.
- Frequent insertion at the **beginning** of a large list is inefficient (O(n) per insert) because every subsequent element must shift.

#### `append()` vs `insert()`

| Aspect | `append()` | `insert()` |
|--------|------------|------------|
| Position | Always adds to the end | Adds at a specified index |
| Performance | O(1) (fast) | O(n) (slower — shifts elements) |
| Syntax | `list.append(item)` | `list.insert(index, item)` |

> **Tip:** Prefer `append()` over `insert(len(list), item)` when adding to the end — it's simpler and more efficient.

---

### `extend()`

#### Definition

`extend()` adds all elements from an **iterable** (list, tuple, string, set, etc.) individually to the end of a list, modifying it in place.

#### Purpose / Why It Is Used

- To merge the contents of another iterable into an existing list without creating a new list object.

#### Syntax

```python
list.extend(iterable)
```

#### Examples

```python
fruits = ["apple", "banana"]
more_fruits = ["cherry", "date"]

fruits.extend(more_fruits)
print(fruits)

# extend() with a string adds each character individually
letters = ["a", "b"]
letters.extend("cd")
print(letters)
```

**Output:**
```
['apple', 'banana', 'cherry', 'date']
['a', 'b', 'c', 'd']
```

**Explanation:** Unlike `append()`, `extend()` unpacks the given iterable and adds each of its elements individually — this is the key distinction between the two methods.

#### `append()` vs `extend()`

```python
list_a = [1, 2, 3]
list_b = [1, 2, 3]

list_a.append([4, 5])
list_b.extend([4, 5])

print(list_a)
print(list_b)
```

**Output:**
```
[1, 2, 3, [4, 5]]
[1, 2, 3, 4, 5]
```

| Method | Adds | Result Length Increase | Example Input `[4, 5]` |
|--------|------|--------------------------|--------------------------|
| `append()` | The entire object as ONE item | Always +1 | Adds `[4, 5]` as a single nested list |
| `extend()` | Each element of the iterable individually | +N (N = number of items) | Adds `4` and `5` as two separate items |

> **Note:** `list.extend(iterable)` behaves the same as `list += iterable` (in-place concatenation), while `list = list + iterable` requires both sides to be lists and creates a new list object.

#### Common Mistakes

```python
fruits = ["apple", "banana"]
# Mistake: Using append() when extend() was intended
fruits.append(["cherry", "date"])
print(fruits)   # Nested list, probably not intended
```

**Output:**
```
['apple', 'banana', ['cherry', 'date']]
```

---

### `remove()`

#### Definition

`remove()` deletes the **first occurrence** of a specified value from the list.

#### Syntax

```python
list.remove(value)
```

#### Examples

```python
numbers = [10, 20, 30, 20, 40]
numbers.remove(20)
print(numbers)   # Only the FIRST 20 is removed
```

**Output:**
```
[10, 30, 20, 40]
```

#### Important Points / Rules

- `remove()` removes by **value**, not by index.
- If the value appears multiple times, only the **first** occurrence is removed.
- If the value is not found, Python raises a `ValueError`.

```python
numbers = [10, 20, 30]
try:
    numbers.remove(99)
except ValueError as e:
    print(f"Error: {e}")
```

**Output:**
```
Error: list.remove(x): x not in list
```

> **Warning:** Always check membership with `in`, or wrap `remove()` in a `try/except`, when the value's presence isn't guaranteed — otherwise your program will crash with a `ValueError`.

#### `remove()` vs `pop()` vs `del`

| Method | Removes By | Returns Removed Item? | Raises Error If Missing/Invalid |
|--------|------------|--------------------------|-----------------------------------|
| `remove(value)` | Value | No (returns `None`) | `ValueError` if value not found |
| `pop(index)` | Index | Yes | `IndexError` if index out of range |
| `del list[index]` | Index | No | `IndexError` if index out of range |

---

### `pop()`

#### Definition

`pop()` removes and **returns** an item at a given index (default: the last item).

#### Syntax

```python
list.pop()          # Removes and returns the last item
list.pop(index)     # Removes and returns the item at the given index
```

#### Examples

```python
fruits = ["apple", "banana", "cherry"]

last_item = fruits.pop()
print(last_item)
print(fruits)

first_item = fruits.pop(0)
print(first_item)
print(fruits)
```

**Output:**
```
cherry
['apple', 'banana']
apple
['banana']
```

**Explanation:** `pop()` is unique among removal methods because it **returns the removed value**, making it useful when you need to use the item after removing it (e.g., implementing a stack).

#### Important Points / Rules

- `pop()` with no arguments removes and returns the **last** element — O(1), very efficient.
- `pop(index)` removes and returns the element at that index — O(n) for indices other than the last, since remaining elements shift.
- Calling `pop()` on an empty list raises an `IndexError`.

```python
empty = []
# empty.pop()   # This would raise: IndexError: pop from empty list
```

#### Real-World Use Cases

- Implementing a **stack** (Last-In-First-Out) using `append()` to push and `pop()` to pop.
- Implementing a simple **queue** using `pop(0)` (though `collections.deque` is more efficient for this).
- Processing and removing items from a to-do list one at a time.

```python
# Stack example
stack = []
stack.append(1)
stack.append(2)
stack.append(3)
print(stack.pop())   # Removes and returns the most recently added item (LIFO)
print(stack)
```

**Output:**
```
3
[1, 2]
```

---

### `reverse()`

#### Definition

`reverse()` reverses the order of elements in a list **in place**.

#### Syntax

```python
list.reverse()
```

#### Examples

```python
numbers = [1, 2, 3, 4, 5]
numbers.reverse()
print(numbers)
```

**Output:**
```
[5, 4, 3, 2, 1]
```

#### Important Points / Rules

- `reverse()` modifies the original list and returns `None`.
- To get a reversed **copy** without modifying the original, use slicing (`list[::-1]`) or the `reversed()` built-in function.

```python
numbers = [1, 2, 3]
reversed_copy = numbers[::-1]
print(numbers)          # Original unchanged
print(reversed_copy)    # New reversed list

# Using the reversed() built-in (returns an iterator)
print(list(reversed(numbers)))
```

**Output:**
```
[1, 2, 3]
[3, 2, 1]
[3, 2, 1]
```

#### `reverse()` vs `[::-1]` vs `reversed()`

| Approach | Modifies Original? | Returns | Use When |
|----------|----------------------|---------|----------|
| `list.reverse()` | Yes (in place) | `None` | You don't need the original order anymore |
| `list[::-1]` | No | New list | You need both the original and reversed versions |
| `reversed(list)` | No | Iterator (needs `list()` to view as a list) | Iterating in reverse without creating a full new list |

#### Common Mistakes

```python
numbers = [1, 2, 3]
numbers = numbers.reverse()   # Mistake: reassigning the None return value
print(numbers)
```

**Output:**
```
None
```

> **Warning:** Just like `append()`, `reverse()` returns `None`. Never write `list = list.reverse()`.

---

### `sort()`

#### Definition

`sort()` arranges the elements of a list **in place**, in ascending order by default.

#### Syntax

```python
list.sort(key=None, reverse=False)
```

| Parameter | Description | Default |
|-----------|-------------|---------|
| `key` | A function applied to each element to determine sort order | `None` |
| `reverse` | If `True`, sorts in descending order | `False` |

#### Examples

```python
numbers = [5, 2, 8, 1, 9]
numbers.sort()
print(numbers)

numbers.sort(reverse=True)
print(numbers)

words = ["banana", "apple", "cherry"]
words.sort()
print(words)
```

**Output:**
```
[1, 2, 5, 8, 9]
[9, 8, 5, 2, 1]
['apple', 'banana', 'cherry']
```

#### Sorting with a `key` Function

```python
words = ["banana", "kiwi", "apple", "fig"]

# Sort by string length instead of alphabetically
words.sort(key=len)
print(words)

# Sort case-insensitively
mixed_case = ["Banana", "apple", "Cherry"]
mixed_case.sort(key=str.lower)
print(mixed_case)

# Sort a list of tuples by the second element
students = [("Amit", 82), ("Priya", 95), ("Rahul", 74)]
students.sort(key=lambda student: student[1])
print(students)
```

**Output:**
```
['fig', 'kiwi', 'apple', 'banana']
['apple', 'Banana', 'Cherry']
[('Rahul', 74), ('Amit', 82), ('Priya', 95)]
```

**Explanation:** The `key` parameter accepts a function that is applied to each element to compute a value used **only** for comparison purposes — the original elements themselves are unchanged in the output, just reordered.

#### `sort()` vs `sorted()`

| Aspect | `list.sort()` | `sorted(list)` |
|--------|-----------------|------------------|
| Modifies original? | Yes (in place) | No |
| Returns | `None` | A new sorted list |
| Works on | Lists only | Any iterable (list, tuple, string, etc.) |

```python
numbers = [3, 1, 2]
result = sorted(numbers)
print(numbers)   # Original unchanged
print(result)    # New sorted list
```

**Output:**
```
[3, 1, 2]
[1, 2, 3]
```

> **Tip:** Use `sorted()` when you need to preserve the original list order elsewhere in your program; use `.sort()` when you no longer need the original order and want to save memory by sorting in place.

#### Common Mistakes

```python
numbers = [3, 1, 2]
numbers = numbers.sort()   # Mistake: sort() returns None
print(numbers)
```

**Output:**
```
None
```

```python
# Mistake: Sorting a list with mixed incomparable types
mixed = [1, "two", 3]
# mixed.sort()   # This would raise: TypeError: '<' not supported between instances of 'str' and 'int'
```

> **Warning:** `sort()` requires all elements to be mutually comparable. Sorting a list containing both numbers and strings raises a `TypeError`.

---

### `count()`

#### Definition

`count()` returns the number of times a specified value appears in the list.

#### Syntax

```python
list.count(value)
```

#### Examples

```python
numbers = [1, 2, 2, 3, 2, 4]
print(numbers.count(2))
print(numbers.count(5))   # Value not present
```

**Output:**
```
3
0
```

#### Real-World Use Cases

- Counting how many times a specific score, grade, or category appears in a dataset.
- Validating data (e.g., checking that a specific status code doesn't appear too many times in a log list).

#### Important Points / Rules

- Returns `0` if the value is not found — never raises an error (unlike `.index()`, covered next).
- Comparison uses `==`, so `1` and `1.0` and `True` are considered equal for counting purposes.

```python
values = [1, True, 1.0, "1"]
print(values.count(1))   # 1, True, and 1.0 are all treated as equal to 1
```

**Output:**
```
3
```

> **Note:** In Python, `True == 1` and `1.0 == 1` both evaluate to `True`, so `count()` treats them as matches. Only the string `"1"` is a genuinely different value.

---

### Membership Testing (`in`, `not in`)

#### Definition

The `in` and `not in` operators check whether a value exists within a list, returning a Boolean.

#### Syntax

```python
value in list
value not in list
```

#### Examples

```python
fruits = ["apple", "banana", "cherry"]

print("banana" in fruits)
print("mango" in fruits)
print("mango" not in fruits)
```

**Output:**
```
True
False
True
```

#### Real-World Use Cases

- Validating whether a selected option exists in a list of allowed values.
- Preventing duplicate entries before appending: `if item not in my_list: my_list.append(item)`.
- Simple access control checks: `if username in authorized_users:`.

#### Important Points / Rules

- Membership testing on a list is **O(n)** — Python checks elements one by one until a match is found or the list ends.
- For frequent membership checks on large collections, a `set` is far more efficient (O(1) average case) than a list.

```python
import time

large_list = list(range(1000000))
large_set = set(large_list)

# Conceptually: checking membership in a list scans up to every element,
# while checking membership in a set uses direct hashing — sets are much
# faster for repeated "is this value present?" checks on large collections.
print(999999 in large_list)
print(999999 in large_set)
```

**Output:**
```
True
True
```

> **Tip:** If you're performing membership checks (`in`) repeatedly inside a loop on a large collection, convert the list to a `set` first for significantly better performance.

### Key Takeaways (List Operations)

- Slicing, concatenation (`+`), and repetition (`*`) all return **new** lists without modifying the originals.
- `append()` adds one item; `extend()` adds each item of an iterable individually — a frequent source of confusion.
- `insert()` adds at a specific index; `remove()` deletes by value; `pop()` deletes by index and returns the removed value; `del` deletes by index without returning anything.
- `reverse()` and `sort()` both modify the list in place and return `None` — never reassign their result.
- `sorted()` and slicing (`[::-1]`) are non-destructive alternatives to `sort()` and `reverse()`.
- `count()` returns occurrence counts safely (returns `0` if absent); `remove()` and `index()` raise errors if the value is missing.
- Membership testing (`in`) is simple but O(n) on lists — use a `set` for frequent lookups on large data.

---

### Other Useful List Methods

A few additional built-in methods round out the core list toolkit.

| Method | Description | Example | Result |
|--------|-------------|---------|--------|
| `index(value)` | Returns index of first occurrence; raises `ValueError` if not found | `[10,20,30].index(20)` | `1` |
| `clear()` | Removes all elements, leaving an empty list | `[1,2,3].clear()` | `[]` |
| `copy()` | Returns a shallow copy of the list | `[1,2,3].copy()` | `[1, 2, 3]` |
| `len(list)` | Built-in function; returns number of elements | `len([1,2,3])` | `3` |

```python
numbers = [10, 20, 30, 20]

print(numbers.index(20))       # First occurrence only
print(numbers.index(20, 2))    # Search starting from index 2

numbers_copy = numbers.copy()
numbers_copy.append(40)
print(numbers)         # Original unaffected
print(numbers_copy)

numbers.clear()
print(numbers)
```

**Output:**
```
1
3
[10, 20, 30, 20]
[10, 20, 30, 20, 40]
[]
```

> **Note:** `index()` behaves like `str.find()`'s stricter counterpart — it raises `ValueError` on failure rather than returning `-1`, so wrap it in `try/except` or check with `in` first if the value's presence isn't guaranteed.

---

## Numerical Operations on List Elements

### Definition

Python provides several built-in functions and techniques for performing calculations — such as totals, extremes, and averages — on numeric values stored in a list.

### Purpose / Why It Is Used

- To analyze numeric datasets: sales figures, exam scores, sensor readings, etc.
- To avoid manually writing loops for common aggregate calculations.
- To transform every element of a list using a mathematical operation.

### `sum()`, `min()`, `max()`

#### Syntax

```python
sum(list)
min(list)
max(list)
```

#### Examples

```python
scores = [85, 92, 78, 90, 88]

print(sum(scores))
print(min(scores))
print(max(scores))
print(len(scores))
```

**Output:**
```
433
78
92
5
```

**Explanation:** `sum()` adds all numeric elements together, `min()`/`max()` find the smallest/largest value, and `len()` (though not numeric-specific) gives the count of elements — all four are commonly combined for statistics.

```python
# sum() with a starting value
total_with_bonus = sum(scores, 10)   # Adds 10 to the total as a starting point
print(total_with_bonus)
```

**Output:**
```
443
```

### Calculating Average

Python has no dedicated built-in "average" function for lists, so it's calculated using `sum()` and `len()`.

```python
scores = [85, 92, 78, 90, 88]
average = sum(scores) / len(scores)
print(average)
print(round(average, 2))
```

**Output:**
```
86.6
86.6
```

> **Warning:** Always guard against dividing by zero when calculating an average of a list that might be empty.

```python
def calculate_average(numbers):
    if len(numbers) == 0:
        return 0
    return sum(numbers) / len(numbers)

print(calculate_average([]))
print(calculate_average([10, 20, 30]))
```

**Output:**
```
0
20.0
```

### List Comprehensions for Numerical Transformations

A **list comprehension** provides a concise way to apply a mathematical operation to every element in a list, producing a new list.

```python
numbers = [1, 2, 3, 4, 5]

squared = [n ** 2 for n in numbers]
doubled = [n * 2 for n in numbers]
incremented = [n + 10 for n in numbers]

print(squared)
print(doubled)
print(incremented)
```

**Output:**
```
[1, 4, 9, 16, 25]
[2, 4, 6, 8, 10]
[11, 12, 13, 14, 15]
```

#### Filtering Numbers with Conditions

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

evens = [n for n in numbers if n % 2 == 0]
odds_squared = [n ** 2 for n in numbers if n % 2 != 0]

print(evens)
print(odds_squared)
```

**Output:**
```
[2, 4, 6, 8, 10]
[1, 9, 25, 49, 81]
```

### Using `map()` for Numerical Operations

`map()` applies a function to every element of a list, returning a **map object** (an iterator), which is typically converted back to a list.

```python
numbers = [1, 2, 3, 4, 5]

squared = list(map(lambda n: n ** 2, numbers))
print(squared)

# Converting a list of strings to integers (common with user input)
str_numbers = ["10", "20", "30"]
int_numbers = list(map(int, str_numbers))
print(int_numbers)
print(sum(int_numbers))
```

**Output:**
```
[1, 4, 9, 16, 25]
[10, 20, 30]
60
```

**Explanation:** `map(int, str_numbers)` applies the `int()` function to each string, converting the whole list from strings to integers — extremely useful when processing numeric input read as text (e.g., from `input()` or a CSV file).

### Comparison: Loop vs List Comprehension vs `map()`

| Approach | Syntax Style | Readability | Returns |
|----------|---------------|--------------|---------|
| `for` loop | Verbose, explicit | Good for complex logic | Builds list manually |
| List comprehension | Concise, Pythonic | Best for simple transformations/filters | New list directly |
| `map()` | Functional style | Good when applying an existing function | Iterator (needs `list()`) |

```python
numbers = [1, 2, 3]

# Traditional loop
result_loop = []
for n in numbers:
    result_loop.append(n * 2)

# List comprehension
result_comprehension = [n * 2 for n in numbers]

# map()
result_map = list(map(lambda n: n * 2, numbers))

print(result_loop)
print(result_comprehension)
print(result_map)
```

**Output:**
```
[2, 4, 6]
[2, 4, 6]
[2, 4, 6]
```

> **Tip:** For simple, single-expression transformations, list comprehensions are generally considered more Pythonic and readable than `map()` with a `lambda`. Reserve `map()` for cases where you're applying an already-named function (like `int` or `str`).

### Real-World Use Cases

- Calculating total sales, average rating, or highest score from a dataset.
- Converting a list of string-based form inputs into numbers for calculation.
- Normalizing or scaling numeric data (e.g., converting Celsius to Fahrenheit for a whole list of temperatures).

```python
celsius_temps = [0, 10, 20, 30, 40]
fahrenheit_temps = [(temp * 9/5) + 32 for temp in celsius_temps]
print(fahrenheit_temps)
```

**Output:**
```
[32.0, 50.0, 68.0, 86.0, 104.0]
```

### Common Mistakes

```python
scores = [85, 92, "78", 90]
# Mistake: Mixed types break numeric operations
# total = sum(scores)   # This would raise: TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

> **Warning:** `sum()`, `min()`, and `max()` require all elements to be of compatible, comparable numeric types. A single string mixed into a numeric list will cause a `TypeError`. Validate or convert data types before performing numeric aggregation.

### Key Takeaways

- `sum()`, `min()`, `max()`, and `len()` are the core built-in tools for numeric list aggregation.
- Average must be calculated manually as `sum(list) / len(list)`, with a check for empty lists to avoid `ZeroDivisionError`.
- List comprehensions are the most Pythonic way to transform or filter numeric lists.
- `map()` is a functional alternative, useful when applying an existing named function like `int()` or `str()` across a list.

---

## Nested Lists

### What Are Nested Lists?

#### Definition

A **nested list** is a list that contains one or more other lists as its elements. This allows you to represent multi-dimensional or hierarchical data, such as grids, matrices, or grouped records.

#### Purpose / Why It Is Used

- To represent tabular data (rows and columns), like a spreadsheet or matrix.
- To group related sub-lists together (e.g., a list of student records, where each record is itself a list).
- To model multi-dimensional data such as coordinates, game boards, or images (as pixel grids).

#### Syntax

```python
nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
print(matrix)
print(len(matrix))        # Number of rows
print(len(matrix[0]))     # Number of columns in the first row
```

**Output:**
```
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
3
3
```

### Accessing Elements in Nested Lists

To access an element inside a nested list, use **multiple indices** — one for each level of nesting.

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(matrix[0])        # First row (a list)
print(matrix[0][0])     # First element of the first row
print(matrix[1][2])     # Third element of the second row
print(matrix[-1][-1])   # Last element of the last row
```

**Output:**
```
[1, 2, 3]
1
6
9
```

**Explanation:** `matrix[row][column]` — the first index selects the row (an inner list), and the second index selects an element within that row.

### Modifying Nested Lists

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

matrix[1][1] = 99
print(matrix)

matrix[0].append(100)
print(matrix)
```

**Output:**
```
[[1, 2, 3], [4, 99, 6], [7, 8, 9]]
[[1, 2, 3, 100], [4, 99, 6], [7, 8, 9]]
```

**Explanation:** Since `matrix[0]` is itself a list, all normal list methods (`append`, `insert`, `remove`, etc.) work directly on it.

### Iterating Through Nested Lists

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Iterating row by row
for row in matrix:
    print(row)

print("---")

# Iterating element by element using nested loops
for row in matrix:
    for value in row:
        print(value, end=" ")
print()

print("---")

# Using nested list comprehension to flatten the matrix
flattened = [value for row in matrix for value in row]
print(flattened)
```

**Output:**
```
[1, 2, 3]
[4, 5, 6]
[7, 8, 9]
---
1 2 3 4 5 6 7 8 9 
---
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

**Explanation:** The nested list comprehension `[value for row in matrix for value in row]` reads left to right, like nested `for` loops: the **outer** loop (`for row in matrix`) runs first, then the **inner** loop (`for value in row`) runs for each row.

### Nested Lists as Matrices

Nested lists are commonly used to represent matrices for mathematical operations.

```python
matrix_a = [
    [1, 2],
    [3, 4]
]
matrix_b = [
    [5, 6],
    [7, 8]
]

# Element-wise addition
result = []
for i in range(len(matrix_a)):
    row = []
    for j in range(len(matrix_a[0])):
        row.append(matrix_a[i][j] + matrix_b[i][j])
    result.append(row)

print(result)
```

**Output:**
```
[[6, 8], [10, 12]]
```

#### Transposing a Matrix (Rows Become Columns)

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6]
]

transposed = [[row[i] for row in matrix] for i in range(len(matrix[0]))]
print(transposed)

# Using zip() — a more Pythonic alternative
transposed_zip = [list(row) for row in zip(*matrix)]
print(transposed_zip)
```

**Output:**
```
[[1, 4], [2, 5], [3, 6]]
[[1, 4], [2, 5], [3, 6]]
```

**Explanation:** `zip(*matrix)` unpacks each row of the matrix as separate arguments to `zip()`, which then groups elements column-wise — a common idiom for transposing nested lists.

> **Note:** For serious numerical/matrix work (large-scale linear algebra), the **NumPy** library is far more efficient and feature-rich than plain nested lists. Nested lists are best suited for small-scale or educational use cases.

### Shallow Copy vs Deep Copy in Nested Lists

This is one of the most important — and most misunderstood — concepts when working with nested lists.

```python
import copy

original = [[1, 2, 3], [4, 5, 6]]

shallow = original.copy()      # or original[:] or list(original)
deep = copy.deepcopy(original)

# Modify an inner list through the shallow copy
shallow[0][0] = 999

print("Original:", original)
print("Shallow:", shallow)
print("Deep:", deep)
```

**Output:**
```
Original: [[999, 2, 3], [4, 5, 6]]
Shallow: [[999, 2, 3], [4, 5, 6]]
Deep: [[1, 2, 3], [4, 5, 6]]
```

**Explanation:** A **shallow copy** creates a new outer list, but the inner lists are still the **same objects** shared between the original and the copy. Modifying an inner list through either reference affects both. A **deep copy** (via `copy.deepcopy()`) recursively copies every nested level, producing a fully independent structure.

| Copy Type | Method | Outer List Independent? | Inner Lists Independent? |
|-----------|--------|----------------------------|------------------------------|
| Assignment (`b = a`) | `b = a` | No (same object) | No (same object) |
| Shallow copy | `a.copy()`, `a[:]`, `list(a)` | Yes | **No** (shared references) |
| Deep copy | `copy.deepcopy(a)` | Yes | Yes |

> **Warning:** This is a very common bug source: developers use `.copy()` expecting full independence, then are surprised when modifying a nested element in the "copy" also changes the original. For nested lists (or any nested mutable structures), use `copy.deepcopy()` when true independence is required.

### Real-World Use Cases

- Representing spreadsheet-like or tabular data (rows and columns).
- Representing a tic-tac-toe or chess board as a grid.
- Storing grouped records: `[["Saurabh", 28], ["Priya", 25]]`.
- Representing image data (a grid of pixel values) in simple image-processing scripts.

### Common Mistakes

```python
# Mistake: The [[0]*3]*3 repetition trap (also covered under Repetition)
board = [[0] * 3] * 3
board[0][0] = "X"
print(board)   # All rows affected, not just the first
```

**Output:**
```
[['X', 0, 0], ['X', 0, 0], ['X', 0, 0]]
```

> **Warning:** As covered earlier under repetition, this happens because all three "rows" are actually the same list object repeated three times. Always build nested lists with a list comprehension: `[[0]*3 for _ in range(3)]`.

### Best Practices

> **Tip:** When building 2D structures, always use `[[default_value] * cols for _ in range(rows)]` — never `[[default_value] * cols] * rows`.

> **Tip:** If you need to pass a nested list to a function and don't want the function to accidentally modify your original data, pass `copy.deepcopy(your_list)` instead of the original.

### Key Takeaways

- Nested lists are lists containing other lists, accessed via `list[row][column]` syntax.
- Iterating nested lists typically uses nested loops or nested list comprehensions.
- `zip(*matrix)` is a Pythonic idiom for transposing a matrix represented as nested lists.
- Shallow copies (`.copy()`, `[:]`) do **not** create independent inner lists — only `copy.deepcopy()` does.
- The `[[value] * cols] * rows` repetition pattern creates shared references and should be avoided in favor of a list comprehension.

---

## Other Related Topics

### List Comprehensions

#### Definition

A **list comprehension** is a concise syntax for creating a new list by applying an expression to each item of an iterable, optionally filtered by a condition.

#### Syntax

```python
[expression for item in iterable if condition]
```

#### Examples

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

squares = [n ** 2 for n in numbers]
even_only = [n for n in numbers if n % 2 == 0]
labeled = ["even" if n % 2 == 0 else "odd" for n in numbers]

print(squares)
print(even_only)
print(labeled)
```

**Output:**
```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
[2, 4, 6, 8, 10]
['odd', 'even', 'odd', 'even', 'odd', 'even', 'odd', 'even', 'odd', 'even']
```

**Explanation:** The `if...else` form (used in `labeled`) is a conditional **expression** evaluated per item and must appear **before** the `for` clause. The filtering `if` (used in `even_only`) appears **after** the `for` clause and simply skips items that don't match.

> **Note:** Don't confuse the two `if` placements: `[expr if cond else expr2 for item in iterable]` transforms every item, while `[expr for item in iterable if cond]` filters which items are included.

#### List Comprehension vs `for` Loop

| Aspect | `for` Loop | List Comprehension |
|--------|------------|----------------------|
| Lines of code | More verbose | Compact, single line |
| Readability for complex logic | Better | Can become hard to read if overused |
| Performance | Slightly slower | Slightly faster (optimized internally) |
| Best for | Multi-step logic, side effects | Simple transformations/filters |

> **Tip:** If a list comprehension needs more than one `if` condition or more than one nested loop, consider switching to a regular `for` loop for the sake of readability.

---

### Copying Lists

#### Definition

Because lists are mutable, simply assigning one list variable to another (`b = a`) does **not** create a copy — it creates a second reference to the **same** list object.

#### Examples

```python
original = [1, 2, 3]
reference = original          # NOT a copy — same object
copy_list = original.copy()   # A true (shallow) copy

reference.append(4)
copy_list.append(99)

print(original)
print(reference)
print(copy_list)
```

**Output:**
```
[1, 2, 3, 4]
[1, 2, 3, 4]
[1, 2, 3, 99]
```

**Explanation:** `reference` and `original` point to the exact same list in memory, so modifying one modifies the other. `copy_list`, created with `.copy()`, is a genuinely separate list object (for simple, non-nested lists).

#### Ways to Copy a List

| Method | Syntax | Notes |
|--------|--------|-------|
| `.copy()` method | `new = old.copy()` | Clearest, most explicit |
| Slicing | `new = old[:]` | Common idiom, same effect as `.copy()` |
| `list()` constructor | `new = list(old)` | Also creates a shallow copy |
| `copy.deepcopy()` | `new = copy.deepcopy(old)` | Required for nested lists needing full independence |

> **Warning:** All of `.copy()`, `[:]`, and `list()` create only a **shallow** copy. For nested lists, refer back to the [Shallow Copy vs Deep Copy](#shallow-copy-vs-deep-copy-in-nested-lists) section.

---

### `len()` and Common Built-in Functions

Beyond the numeric functions already covered, a few general-purpose built-ins are used constantly with lists.

| Function | Description | Example | Result |
|----------|-------------|---------|--------|
| `len(list)` | Number of elements | `len([1,2,3])` | `3` |
| `type(list)` | Returns the data type | `type([1,2,3])` | `<class 'list'>` |
| `list(iterable)` | Converts an iterable to a list | `list("abc")` | `['a','b','c']` |
| `enumerate(list)` | Pairs each item with its index | see below | — |

```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(index, fruit)

for index, fruit in enumerate(fruits, start=1):
    print(index, fruit)
```

**Output:**
```
0 apple
1 banana
2 cherry
1 apple
2 banana
3 cherry
```

> **Tip:** Use `enumerate()` instead of manually managing a counter variable (`i = 0; i += 1`) when you need both the index and the value while looping.

### Key Takeaways

- List comprehensions offer a concise, Pythonic alternative to `for` loops for building new lists.
- `b = a` does not copy a list — it creates a second reference to the same object; use `.copy()`, `[:]`, or `copy.deepcopy()` as appropriate.
- `enumerate()` is the idiomatic way to loop with both index and value.

---

## Overall Summary

This document covered Python lists from the ground up:

- **Introduction** established what lists are — ordered, mutable, indexable collections — and how they compare to tuples, sets, and dictionaries.
- **List operations** covered slicing, concatenation, and repetition (all non-destructive), alongside the core mutating methods: `append()`, `insert()`, `extend()`, `remove()`, `pop()`, `reverse()`, `sort()`, `count()`, and membership testing with `in`.
- **Numerical operations** showed how to use `sum()`, `min()`, `max()`, list comprehensions, and `map()` to analyze and transform numeric data stored in lists.
- **Nested lists** introduced multi-dimensional data structures, matrix-style operations, and the critical distinction between shallow and deep copies.
- **Related topics** rounded out the toolkit with list comprehensions, list copying strategies, and useful built-ins like `enumerate()`.

Together, these form the essential foundation for working with collections of data in Python — a skill used in virtually every non-trivial Python program.

---

## Quick Revision / Cheat Sheet

```python
# ---------- CREATION ----------
my_list = [1, 2, 3]
empty = []
from_range = list(range(5))

# ---------- SLICING / CONCAT / REPETITION ----------
my_list[1:3]        # slice
my_list[::-1]        # reversed copy
list1 + list2         # concatenation (new list)
[0] * 5               # repetition
[[0]*3 for _ in range(3)]   # correct way to build a 2D grid

# ---------- ADDING ITEMS ----------
my_list.append(x)          # add one item at the end
my_list.insert(i, x)       # add one item at index i
my_list.extend(iterable)   # add each item of iterable individually

# ---------- REMOVING ITEMS ----------
my_list.remove(value)   # remove first occurrence by value (ValueError if missing)
my_list.pop()            # remove & return last item
my_list.pop(i)            # remove & return item at index i
del my_list[i]             # remove item at index i (no return)
my_list.clear()            # remove all items

# ---------- REORDERING ----------
my_list.reverse()               # reverse in place
my_list.sort()                   # sort in place, ascending
my_list.sort(reverse=True)       # sort in place, descending
my_list.sort(key=func)           # sort using a key function
sorted(my_list)                   # NEW sorted list, original unchanged

# ---------- SEARCHING / COUNTING ----------
value in my_list        # membership check (Boolean)
my_list.count(value)     # count occurrences
my_list.index(value)     # index of first occurrence (ValueError if missing)

# ---------- NUMERIC OPERATIONS ----------
sum(my_list)
min(my_list)
max(my_list)
len(my_list)
sum(my_list) / len(my_list)   # average (guard against division by zero)

# ---------- COPYING ----------
new = my_list.copy()          # shallow copy
new = my_list[:]                # shallow copy (slicing)
import copy
new = copy.deepcopy(my_list)    # deep copy (for nested lists)

# ---------- COMPREHENSIONS ----------
[x**2 for x in my_list]
[x for x in my_list if x % 2 == 0]
[x if x > 0 else 0 for x in my_list]
```

| Method | Modifies In Place? | Returns |
|--------|----------------------|---------|
| `append()` | Yes | `None` |
| `insert()` | Yes | `None` |
| `extend()` | Yes | `None` |
| `remove()` | Yes | `None` |
| `pop()` | Yes | Removed item |
| `reverse()` | Yes | `None` |
| `sort()` | Yes | `None` |
| `count()` | No | Integer |
| `index()` | No | Integer |
| `copy()` | No | New list |

---

## Common Interview Questions

**1. What is the difference between `append()` and `extend()`?**
`append()` adds its argument as a single element, even if that argument is itself a list — resulting in a nested list. `extend()` iterates over its argument and adds each element individually, effectively merging two lists.

**2. What is the difference between `remove()` and `pop()`?**
`remove()` deletes an element by its **value** (the first matching occurrence) and returns `None`. `pop()` deletes an element by its **index** (defaulting to the last item) and returns the removed value, making it useful when the removed item is still needed.

**3. Why does `[[0] * 3] * 3` produce a "broken" 2D list?**
Because the outer `*` repeats **references** to the same inner list object three times, rather than creating three independent lists. Modifying one row modifies all of them. The fix is to use a list comprehension: `[[0] * 3 for _ in range(3)]`.

**4. What is the difference between a shallow copy and a deep copy?**
A shallow copy (`.copy()`, `[:]`, `list()`) creates a new outer list but keeps references to the same inner objects for nested structures — mutating a nested list affects both the original and the copy. A deep copy (`copy.deepcopy()`) recursively duplicates every level, producing a fully independent structure.

**5. What is the difference between `sort()` and `sorted()`?**
`sort()` is a list method that sorts the list **in place** and returns `None`. `sorted()` is a built-in function that works on any iterable and returns a **new** sorted list, leaving the original unchanged.

**6. How would you remove duplicates from a list?**
The most common approach is converting the list to a `set` and back: `list(set(my_list))`. Note this doesn't preserve order (though in modern Python, `dict.fromkeys(my_list)` can be used to remove duplicates while preserving order).

**7. Why does list membership testing (`in`) get slow on large lists?**
Because `in` on a list performs a linear scan — O(n) in the worst case — checking each element until a match is found or the list ends. For frequent membership checks on large collections, converting to a `set` (O(1) average lookup) is much faster.

**8. How do you flatten a nested list of arbitrary depth?**
For a simple 2D nested list, a nested list comprehension works: `[val for row in matrix for val in row]`. For arbitrarily deep nesting, a recursive function is typically required.

**9. What happens if you call `.pop()` on an empty list?**
It raises an `IndexError: pop from empty list`. Always check `if my_list:` before popping if the list might be empty.

**10. How do you sort a list of tuples by a specific element?**
Use the `key` parameter with a function (often a `lambda`) that extracts the relevant element: `my_list.sort(key=lambda item: item[1])` sorts by each tuple's second element.

---

## Practice Exercises

1. Create a list of 5 numbers and use slicing to print only the middle 3 elements.
2. Given `list_a = [1, 2, 3]` and `list_b = [4, 5, 6]`, produce a combined list using concatenation, without modifying either original list.
3. Write code that correctly builds a 3x3 grid of zeros where changing one cell does not affect the others.
4. Given `fruits = ["apple", "banana"]`, demonstrate the difference in output between `fruits.append(["cherry","date"])` and `fruits.extend(["cherry","date"])` on two separate copies of the list.
5. Write a function that safely removes a value from a list using `remove()`, without crashing if the value isn't present.
6. Implement a simple stack using `append()` and `pop()` that pushes the numbers 1 through 5, then pops and prints them one at a time.
7. Given `scores = [45, 89, 67, 92, 34, 78]`, calculate and print the sum, minimum, maximum, and average.
8. Write a list comprehension that returns only the even squares from `range(1, 20)`.
9. Given a nested list `students = [["Amit", 82], ["Priya", 95], ["Rahul", 74]]`, sort it by score in descending order using `sort()` with a `key`.
10. Demonstrate the shallow copy vs deep copy difference: create a nested list, make a shallow copy with `.copy()`, modify an inner list through the copy, and show that the original is also affected. Then repeat using `copy.deepcopy()` and show that the original is unaffected.
11. Write code to transpose a 2x3 matrix using `zip()`.
12. Explain (in your own words) why `numbers = numbers.sort()` results in `numbers` becoming `None`.

> **Tip:** Test each solution in a Python interpreter and compare your output against the explanations and rules covered in this document.
