# Exercise Solutions: Repeat with For and Range

```python
for number in range(1, 11):
    print(number)

for number in range(10, 0, -2):
    print(number)

for position, character in enumerate("Python", start=1):
    print(position, character)

for letter, number in zip("ABC", range(1, 4), strict=True):
    print(letter, number)

total = 0
for number in range(1, 101):
    total += number
print(total)
print(sum(range(1, 101)))
```

Both totals are 5050.
