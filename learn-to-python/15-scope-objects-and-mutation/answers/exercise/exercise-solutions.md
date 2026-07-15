# Exercise Solutions: Names, Scope, Objects, and Mutation

```python
TAX_RATE = 0.08

def hidden_total(amount):
    return amount * (1 + TAX_RATE)

def explicit_total(amount, tax_rate):
    return amount * (1 + tax_rate)

def mutate(values):
    values.append(3)

def rebind(values):
    values = [99]
    return values

original = [1, 2]
mutate(original)
replacement = rebind(original)
print(original, replacement)

first = [1, 2]
second = [1, 2]
print(first == second, first is second)

nested = [[1], [2]]
copied = nested.copy()
copied[0].append(9)
print(nested, copied)

def increment(count):
    return count + 1

count = increment(0)
```

The returned count makes the state transition explicit.
