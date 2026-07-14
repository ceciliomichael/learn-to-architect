# Exercise Solutions: Lists and Mutation

```python
tasks = ["read"]
tasks.append("practice")
tasks.append("review")
tasks.insert(0, "plan")
tasks[1] = "read lesson"
completed = tasks.pop(0)

alias = tasks
alias.append("shared change")
print(tasks, alias)

copied = tasks.copy()
copied.append("copy only")
print(tasks, copied)

values = [3, 1, 2]
ordered = sorted(values)
sort_result = values.sort()
print(ordered, values, sort_result)

positive = []
for number in [-2, 0, 3, 5]:
    if number > 0:
        positive.append(number)
print(positive)

colors = "red,green,blue".split(",")
print(colors)
print(" | ".join(colors))
```

The alias shares changes. The copied outer list does not. In-place sort returns `None`. Splitting creates three list items, and joining produces `red | green | blue` without changing that list.
