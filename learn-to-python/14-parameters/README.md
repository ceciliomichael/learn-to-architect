# Module 14: Use Parameters Clearly

## What you will learn

You will control how callers supply arguments and avoid reused mutable defaults.

## Positional and keyword arguments

```python
def describe(name, price):
    return f"{name}: {price:.2f}"

describe("Pen", 1.25)
describe(name="Pen", price=1.25)
```

Keywords improve clarity. Positional arguments are concise when meaning is obvious and order is stable.

## Defaults are created once

```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"
```

Parameters with defaults follow required positional parameters.

Never use a mutable object as a default unless shared state is intentional:

```python
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
```

Default expressions run when the function is defined, not once per call. A default list would be reused.

## Require keyword clarity

```python
def create_user(name, *, active=True, role="reader"):
    return {"name": name, "active": active, "role": role}
```

Arguments after `*` are keyword-only. This prevents unclear calls such as `create_user("Ava", False, "owner")`.

Parameters before `/` are positional-only:

```python
def ratio(numerator, denominator, /):
    return numerator / denominator
```

Use this mainly when parameter names should not become part of the public calling contract.

## Collect variable arguments

```python
def total(*values):
    return sum(values)

def build_record(name, **fields):
    return {"name": name, **fields}
```

`*values` is a tuple. `**fields` is a dictionary with string keys from keyword arguments. These features can hide an unclear interface, so use explicit parameters when the accepted fields are known.

## Unpack calls

```python
dimensions = (4, 5)
print(area(*dimensions))

options = {"active": False, "role": "editor"}
print(create_user("Ben", **options))
```

The lengths and names must match the function contract.

## Check your understanding

You are ready when you can design keyword-only options and explain why `None` prevents a mutable default leak.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
