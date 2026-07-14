# Module 17: Handle Exceptions Deliberately

## What you will learn

You will catch expected failures narrowly, raise clear built-in errors, and preserve useful error information.

## Exceptions report failure

Syntax errors prevent code from being parsed. Exceptions happen while valid syntax executes. A traceback shows the call path, exception type, and message.

Catch only a failure you can handle:

```python
text = input("Whole number: ")
try:
    number = int(text)
except ValueError:
    print("Enter a valid whole number.")
else:
    print(number * 2)
```

The `try` block stays small. `else` runs only when no exception occurs. This prevents an unrelated `ValueError` in later work from being mislabeled as bad input.

## Use finally for unavoidable cleanup

```python
resource = acquire_resource()
try:
    use_resource(resource)
finally:
    resource.close()
```

`finally` runs whether the try succeeds, returns, or raises. Prefer context managers when available, taught in Modules 18 and 31.

## Catch specific types

```python
try:
    value = mapping[key]
except KeyError:
    value = "missing"
```

Avoid bare `except:` and broad `except Exception` around large blocks. They can hide programming defects and shutdown signals. Catch several expected types separately when recovery differs.

## Raise a clear contract error

```python
def percentage(part, whole):
    if whole <= 0:
        raise ValueError("whole must be greater than zero")
    return part / whole * 100
```

Raise built-in exceptions when their meaning fits. Custom exception classes are introduced after ordinary classes in Module 23.

## Preserve causes

```python
try:
    quantity = int(text)
except ValueError as error:
    raise ValueError("quantity must be a whole number") from error
```

`from error` records the original cause. `raise` alone inside an exception handler reraises the current exception with its traceback.

## Never use exceptions as silent defaults

```python
# Harmful: hides every failure.
try:
    important_work()
except Exception:
    pass
```

Recover, add context and reraise, or let the failure reach a boundary that can report it. Logs and user messages have different audiences and should not expose secrets.

## Check your understanding

You are ready when you can minimize a try block, choose a specific exception, and explain else, finally, and chaining.
