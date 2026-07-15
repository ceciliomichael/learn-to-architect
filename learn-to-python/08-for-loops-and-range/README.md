# Module 08: Repeat with For and Range

## What you will learn

You will iterate over existing items, generate integer sequences, and loop over paired data.

## For visits an iterable

```python
for letter in "Python":
    print(letter)
```

Python asks the string for its items and binds `letter` to each one. Use `for` when iterating over a known iterable. Use `while` when repetition depends mainly on a changing condition.

## Generate integers with range

```python
for number in range(5):
    print(number)
```

This prints 0 through 4. The stop is excluded.

```python
range(2, 6)      # 2, 3, 4, 5
range(10, 0, -2) # 10, 8, 6, 4, 2
```

`range` is a compact iterable, not a prebuilt list.

## Keep an index with enumerate

```python
for position, letter in enumerate("Python", start=1):
    print(position, letter)
```

Prefer `enumerate` over managing a separate counter.

## Pair iterables with zip

```python
letters = "ABC"
for letter, number in zip(letters, range(1, 4)):
    print(letter, number)
```

Ordinary `zip` stops at the shortest iterable. In Python 3.10 and newer, passing `strict=True` to `zip` raises `ValueError` if lengths differ, which is safer when every item needs a partner.

## Accumulate deliberately

```python
total = 0
for number in range(1, 5):
    total += number
print(total)
```

Initialize the accumulator before the loop and update it once per intended item.

Loop `else`, `break`, and `continue` behave as they do for while loops.

## Check your understanding

You are ready when you can predict a range, choose for or while, and explain shortest-input zip behavior.
