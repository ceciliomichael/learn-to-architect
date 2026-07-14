# Exercise Solutions: Sets and Membership

```python
required = {"variables", "conditions", "loops"}
completed = {"variables", "conditions"}
print(required - completed)
print(required & completed)
print(required | completed)
print(completed <= required)

completed.add("loops")
completed.discard("missing")

try:
    completed.remove("missing")
except KeyError:
    print("remove requires the value to exist")

names = ["Ava", "Ben", "Ava", "Cleo"]
unique_in_order = list(dict.fromkeys(names))
print(unique_in_order)

permissions = frozenset({"read", "write"})
labels = {permissions: "editor"}
print(labels[permissions])
```

The handled `KeyError` demonstrates that `remove` requires the member to exist. Use `discard` when absence is acceptable.
