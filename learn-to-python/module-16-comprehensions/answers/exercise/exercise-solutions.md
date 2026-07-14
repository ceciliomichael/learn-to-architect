# Exercise Solutions: Comprehensions and Generator Expressions

```python
raw_names = [" Ava ", "", " Ben"]
names = [name.strip().upper() for name in raw_names if name.strip()]
print(names)

lengths = {len(word) for word in ["a", "to", "tea", "be"]}
print(lengths)

cubes = {number: number ** 3 for number in range(1, 6)}
print(cubes)

labels = ["even" if number % 2 == 0 else "odd" for number in range(10)]
print(labels)

values = (number * number for number in range(5))
print(sum(values))
print(sum(values))
```

The second generator sum is zero because the first consumption exhausted it.
