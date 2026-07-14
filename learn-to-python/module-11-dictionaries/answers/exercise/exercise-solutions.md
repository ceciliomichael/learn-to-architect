# Exercise Solutions: Dictionaries

```python
student = {"student_id": 7, "name": "Ava", "score": 82}
student["active"] = True
student["score"] = 88

print(student["name"])
print(student.get("nickname", "No nickname"))

for key, value in student.items():
    print(key, value)

defaults = {"theme": "light", "page_size": 20}
user = {"page_size": 50}
settings = defaults | user
print(settings)

original = {"tags": ["new"]}
copied = original.copy()
copied["tags"].append("sale")
print(original)
print(copied)
```

Both final dictionaries show the added tag because their `tags` values refer to the same list.
