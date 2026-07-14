# Exercise Solutions: Define and Call Functions

```python
def area(width, height):
    return width * height

def is_even(number):
    return number % 2 == 0

def format_price(amount):
    return f"{amount:.2f}"

def subtotal(price, quantity):
    return price * quantity

def add_tax(amount, tax_rate):
    return amount * (1 + tax_rate)

before_tax = subtotal(12.5, 3)
after_tax = add_tax(before_tax, 0.08)
print(format_price(after_tax))

def announce():
    print("Ready")

result = announce()
print(result)

def smallest_and_largest(numbers):
    return min(numbers), max(numbers)

smallest, largest = smallest_and_largest([8, 2, 11])
print(smallest, largest)
```

The announcement result is `None` because `announce` has no explicit return. The final function returns one tuple, which the caller unpacks into two names.
