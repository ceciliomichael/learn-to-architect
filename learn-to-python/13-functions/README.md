# Module 13: Define and Call Functions

## What you will learn

You will name reusable behavior, pass input, return output, and split a program into understandable pieces.

## Define and call

```python
def greet(name):
    """Return a greeting for one name."""
    return f"Hello, {name}!"

message = greet("Ava")
print(message)
```

`def` creates a function object and binds its name. A parameter receives a call argument. `return` ends the call and sends one object back.

Printing and returning are different. Printing creates output. Returning lets the caller decide what to do.

## No explicit return means None

```python
def show_status():
    print("Ready")

result = show_status()
print(result)  # None
```

Use a side-effecting function when output is its job. Use returned values for calculations that should be reusable and testable.

## Return early for clear boundaries

```python
def shipping_cost(order_total):
    if order_total < 0:
        return None
    if order_total >= 100:
        return 0
    return 10
```

The caller must understand what `None` means. Later exceptions can represent invalid input more clearly.

## Functions create local names

Names assigned inside a function are normally local to that call:

```python
def calculate_total(price, quantity):
    subtotal = price * quantity
    return subtotal
```

`subtotal` is unavailable outside. Module 15 explains scope and shared mutable objects fully.

## Return several related values

A function always returns one object. Commas can create one tuple, which the caller can unpack:

```python
def smallest_and_largest(numbers):
    return min(numbers), max(numbers)

smallest, largest = smallest_and_largest([8, 2, 11])
print(smallest, largest)
```

Use this for a small, closely related result. A named data structure becomes clearer when many positions need explanation.

## Decompose by responsibility

Prefer a function with one clear purpose and a name that says what it returns or does. Avoid functions controlled by unrelated boolean flags. Compose small results:

```python
def subtotal(price, quantity):
    return price * quantity

def add_tax(amount, tax_rate):
    return amount * (1 + tax_rate)
```

## Docstrings explain a public contract

The first string in a function is its docstring. Explain purpose, important input rules, return meaning, and raised exceptions. Do not narrate obvious syntax.

## Check your understanding

You are ready when you can distinguish argument, parameter, print, and return and write one focused function.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
