# Exercise Solutions: Input and Conversion

```python
name = input("Name: ")
print(f"Hello, {name}!")

first = int(input("First whole number: "))
second = int(input("Second whole number: "))
print(first + second)

quantity = int(input("Quantity: "))
price = float(input("Unit price: "))
print(f"Subtotal: {quantity * price:.2f}")

print("3" + "4")
print(int("3") + int("4"))
```

The final outputs are `34` and `7`. Invalid integer text raises `ValueError` because it has no valid whole-number representation.
