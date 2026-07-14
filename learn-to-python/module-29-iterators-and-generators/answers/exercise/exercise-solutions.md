# Exercise Solutions: Iterators and Generators

```python
iterator = iter([10, 20])
while True:
    try:
        print(next(iterator))
    except StopIteration:
        break

def inclusive_range(start: int, stop: int, step: int = 1):
    if step <= 0:
        raise ValueError("step must be positive")
    current = start
    while current <= stop:
        yield current
        current += step

def cleaned_lines(lines):
    for line in lines:
        cleaned = line.strip()
        if cleaned:
            yield cleaned

def combined():
    yield from inclusive_range(1, 3)
    yield from inclusive_range(10, 12)

large = (number * number for number in range(1_000_000))
for _ in range(3):
    print(next(large))
```

Only three square values are requested; later values remain uncomputed.
