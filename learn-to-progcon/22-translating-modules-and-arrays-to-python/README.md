# Module 22: Translating Modules and Arrays to Python

## Before you start

Complete Modules 01 to 21. You should understand hierarchy charts, arrays, linear search, and Python control flow.

## What you will learn

- write Python functions that act like design modules
- pass data with parameters and return results
- use lists as arrays with 0-based indexes
- loop through lists by item and by index
- implement linear search and parallel lists in Python
- translate a small modular design into a complete program

## Why this matters

Your earlier hierarchy charts and array designs become cleaner Python when functions and lists match those ideas one for one.

## 1. Functions as modules

A **function** is a named block of code. In ProgCon terms, it is a module you can call.

```python
def greet():
    print("Welcome")


greet()
```

- `def` starts a function definition
- the name is `greet`
- parentheses hold parameters (none here)
- the indented body runs when the function is called

## 2. Parameters and return values

**Parameters** are names that receive input values when the function is called.

A **return value** sends a result back to the caller.

```python
def add_tax(price):
    total = price * 1.10
    return total


bill = add_tax(50)
print(bill)
```

Output:

```text
55.0
```

Mapping:

| Design idea | Python |
| --- | --- |
| module header with inputs | `def name(param1, param2):` |
| module result | `return value` |
| call module | `name(arguments)` |

## 3. Lists as arrays

A Python **list** stores an ordered collection of values.

```python
scores = [80, 90, 70, 85]
print(scores[0])
print(scores[2])
scores[1] = 95
print(scores)
```

Output:

```text
80
70
[80, 95, 70, 85]
```

Indexes start at 0. `len(scores)` is the size.

```python
print(len(scores))
```

## 4. Loop through a list

By value:

```python
prices = [10, 4, 7]
for price in prices:
    print(price)
```

By index:

```python
prices = [10, 4, 7]
for index in range(len(prices)):
    print(index, prices[index])
```

Use index loops when you need the position, especially with parallel lists.

## 5. Growing a list

```python
names = []
names.append("Ana")
names.append("Ben")
print(names)
```

`append` adds one element at the end. This is useful when you gather values during input.

## 6. Linear search in Python

```python
def find_index(items, target):
    index = 0
    while index < len(items):
        if items[index] == target:
            return index
        index = index + 1
    return -1


products = ["Tea", "Bread", "Milk"]
position = find_index(products, "Bread")
if position == -1:
    print("Not found")
else:
    print("Found at", position)
```

Returning `-1` is a common way to mean "not found."

## 7. Parallel lists

```python
products = ["Tea", "Bread", "Milk"]
prices = [3.5, 2.0, 1.5]

name = input("Product: ")
position = find_index(products, name)
if position == -1:
    print("Product not found")
else:
    print("Price:", prices[position])
```

Keep the lists the same length and update them together.

## 8. Full modular program

Design goal: read three scores, return the average from a function, then print Pass or Review.

```python
def read_scores(count):
    values = []
    for n in range(count):
        text = input("Enter score: ")
        values.append(float(text))
    return values


def average_of(values):
    total = 0.0
    for value in values:
        total = total + value
    return total / len(values)


def main():
    scores = read_scores(3)
    avg = average_of(scores)
    print("Average:", avg)
    if avg >= 75:
        print("Pass")
    else:
        print("Review")


main()
```

`main` acts like your main module. Other functions are the lower modules on a hierarchy chart.

## Predict the result

```python
nums = [2, 4, 6]
print(nums[1])
print(len(nums))
```

Expected:

```text
4
3
```

## Common mistakes

### Forgetting to call the function

Defining `def main():` does not run it until you write `main()`.

### Mixing up return and print

`print` shows a value. `return` sends a value back to the caller. A function may do either or both, but they are not the same.

### Using a missing index

Valid indexes are `0` through `len(list) - 1`.

### Changing only one parallel list

If products and prices are paired, update both at the same index.

## Check your understanding

1. What keyword defines a function in Python?
2. What does `return` do?
3. If `colors = ["red", "green"]`, what is `colors[0]`?
4. How do you get the number of elements in a list?
5. Why is `main()` useful as a top-level module?

## Practice

Complete the [module exercises](./exercise/exercise.md). Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 23](../23-capstone-design-and-build/README.md), you will complete a full design-to-Python project.
