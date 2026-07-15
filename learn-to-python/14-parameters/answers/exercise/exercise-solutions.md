# Exercise Solutions: Use Parameters Clearly

```python
def label(name, *, uppercase=False, prefix=""):
    text = name.upper() if uppercase else name
    return prefix + text

def collect(value, values=None):
    if values is None:
        values = []
    values.append(value)
    return values

first = collect(1)
second = collect(2)
print(first, second)

def total(*values):
    return sum(values)

def record(name, **fields):
    return {"name": name, **fields}

print(total(*(2, 3, 4)))
print(record("Ava", **{"role": "editor", "active": True}))
```

The two collection calls return separate lists because each call creates a list when it receives `None`.
