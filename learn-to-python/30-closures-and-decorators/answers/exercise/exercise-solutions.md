# Exercise Solutions: Closures and Decorators

```python
from functools import wraps

def make_multiplier(factor: int):
    def multiply(value: int) -> int:
        return factor * value
    return multiply

def make_counter():
    count = 0
    def next_count() -> int:
        nonlocal count
        count += 1
        return count
    return next_count

def count_calls(function):
    calls = 0
    @wraps(function)
    def wrapper(*args, **kwargs):
        nonlocal calls
        calls += 1
        print(f"call {calls}")
        return function(*args, **kwargs)
    return wrapper

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

double = make_multiplier(2)
first_counter = make_counter()
second_counter = make_counter()
print(double(5), first_counter(), first_counter(), second_counter())

events: list[str] = []

def outer(function):
    events.append("apply outer")
    @wraps(function)
    def wrapper(*args, **kwargs):
        events.append("call outer start")
        result = function(*args, **kwargs)
        events.append("call outer end")
        return result
    return wrapper

def inner(function):
    events.append("apply inner")
    @wraps(function)
    def wrapper(*args, **kwargs):
        events.append("call inner start")
        result = function(*args, **kwargs)
        events.append("call inner end")
        return result
    return wrapper

@outer
@inner
def greet() -> str:
    events.append("call greet")
    return "hello"

print(events)
events.clear()
print(greet())
print(events)
```

Each counter closure owns a distinct enclosing `count` binding. `count_calls` preserves the wrapped return value and metadata. `repeat` validates its configuration before creating a wrapper.

For the stacked decorators, `inner` is applied first and `outer` second. During the call, the outer wrapper starts first, then the inner wrapper, then the function. The wrappers finish in the reverse direction.
