# Exercise Solutions: Text and String Operations

```python
raw = "  Python Course  "
cleaned = raw.strip()
print(f"[{raw}]")
print(f"[{cleaned}]")

language = "TypeScript"
print(language[0])
print(language[-1])
print(language[2:8])

colors = "red,green,blue"
print(colors.replace(",", " | "))

item = "Notebook"
quantity = 3
unit_price = 4.25
subtotal = quantity * unit_price
print(f"{quantity} x {item} at {unit_price:.2f} = {subtotal:.2f}")
```

The original text retains its spaces because strings are immutable and `strip` returned a new string.
