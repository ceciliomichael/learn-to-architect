# Exercise Solutions: Handle Exceptions Deliberately

```python
while True:
    try:
        number = int(input("Whole number: "))
    except ValueError:
        print("Use whole-number digits.")
    else:
        break

def divide(numerator, denominator):
    return numerator / denominator

try:
    print(divide(10, 0))
except ZeroDivisionError:
    print("The denominator must not be zero.")

def validate_quantity(quantity):
    if quantity < 0:
        raise ValueError("quantity must not be negative")

def reserve(requested, available):
    if requested > available:
        raise ValueError(
            f"requested {requested}, available {available}"
        )

def required_setting(settings, name):
    try:
        return settings[name]
    except KeyError as error:
        raise ValueError(f"missing setting: {name}") from error
```

Each handler covers only the expected operation and keeps the original cause where useful.
