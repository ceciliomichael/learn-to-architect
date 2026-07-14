# Module 10: Tuples and Unpacking

## What you will learn

You will use fixed ordered records and unpack their values clearly.

## A tuple is an ordered sequence

```python
location = (14.6, 121.0)
print(location[0])
print(location[-1])
```

Tuples support length, indexing, slicing, iteration, membership, and comparison. Unlike lists, tuples do not allow item assignment, append, or removal.

```python
# This raises TypeError.
location[0] = 15.0
```

Immutability makes a tuple useful for a fixed group whose positions have known meanings.

## Commas create tuples

```python
empty = ()
one_item = ("only",)
also_a_tuple = "red", "green", "blue"
```

The trailing comma is required for a one-item tuple. Parentheses mainly improve grouping and readability.

## Unpack matching positions

```python
latitude, longitude = location
print(latitude)
print(longitude)
```

The target count must match unless one target is starred:

```python
first, *middle, last = (10, 20, 30, 40)
```

`first` is 10, `middle` is the list `[20, 30]`, and `last` is 40.

Swap names without a temporary name:

```python
left, right = right, left
```

Python evaluates the right side before binding the left targets.

## Tuple immutability is shallow

```python
record = ("Ava", [80, 90])
record[1].append(100)
```

The tuple still refers to the same list, but that list is mutable. A tuple prevents replacing its item references; it does not freeze nested objects.

## Use named structures when positions become unclear

`("Ava", 20, True)` forces readers to remember positions. A dictionary, dataclass, or named record can express fields more clearly. Choose a tuple for small, stable, obvious positions.

## Common mistakes

- Omitting the comma from a one-item tuple.
- Unpacking the wrong number of values.
- Believing a tuple makes nested lists immutable.
- Returning many unrelated values instead of modeling a clear result.

## Check your understanding

You are ready when you can create a one-item tuple, unpack fixed and starred targets, and explain shallow immutability.
