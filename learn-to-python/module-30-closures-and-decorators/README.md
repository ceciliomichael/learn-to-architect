# Module 30: Closures and Decorators

## What you will learn

You will retain enclosing state and wrap functions without losing their identity or contract.

## Functions are objects

They can be assigned, passed, and returned:

```python
def upper(text: str) -> str:
    return text.upper()

transform = upper
print(transform("ready"))
```

## A closure remembers enclosing bindings

```python
def make_prefixer(prefix: str):
    def add_prefix(text: str) -> str:
        return prefix + text
    return add_prefix

warn = make_prefixer("Warning: ")
print(warn("low stock"))
```

The returned function retains access to `prefix` even after the outer call ends.

Use `nonlocal` only when the inner function must rebind enclosing state:

```python
def make_counter():
    count = 0
    def next_count():
        nonlocal count
        count += 1
        return count
    return next_count
```

Stateful closures can be useful but require the same concurrency and testing care as mutable objects.

## A decorator replaces a function with a wrapper

```python
from functools import wraps

def trace(function):
    @wraps(function)
    def wrapper(*args, **kwargs):
        print(f"Calling {function.__name__}")
        return function(*args, **kwargs)
    return wrapper

@trace
def greet(name: str) -> str:
    return f"Hello, {name}"
```

Decoration is equivalent to `greet = trace(greet)` at definition time. `wraps` preserves name, docstring, annotations, and a link used by introspection.

## Decorator factories accept configuration

```python
def repeat(times: int):
    if times < 1:
        raise ValueError("times must be positive")
    def decorate(function):
        @wraps(function)
        def wrapper(*args, **kwargs):
            result = None
            for _ in range(times):
                result = function(*args, **kwargs)
            return result
        return wrapper
    return decorate
```

Three levels represent configuration, function decoration, and each call.

## Keep wrappers transparent

Preserve return values and exceptions unless changing them is the documented purpose. Never log passwords, tokens, or sensitive arguments. Decorator order matters: the decorator closest to `def` is applied first.

## Check your understanding

You are ready when you can draw closure lifetime and expand decorator syntax into ordinary assignment.
