# Module 16: Comprehensions and Generator Expressions

## What you will learn

You will create collections from readable transformations and use lazy expressions when a full list is unnecessary.

## Translate a clear loop

Ordinary loop:

```python
squares = []
for number in range(1, 6):
    squares.append(number * number)
```

Equivalent list comprehension:

```python
squares = [number * number for number in range(1, 6)]
```

Read it as expression, for clause, then optional filter.

```python
even_squares = [
    number * number
    for number in range(1, 11)
    if number % 2 == 0
]
```

Use a comprehension only when one transformation and filter remain easier to understand than the loop.

## Set and dictionary comprehensions

```python
first_letters = {name[0] for name in ["Ava", "Ben", "Ana"]}

lengths = {name: len(name) for name in ["Ava", "Benjamin"]}
```

Duplicate set results collapse. Duplicate dictionary keys keep the last generated value, so confirm uniqueness when overwriting would hide data.

## Choose expression versus filter

This chooses a value for every input:

```python
labels = ["even" if number % 2 == 0 else "odd" for number in range(4)]
```

This keeps only some inputs:

```python
evens = [number for number in range(4) if number % 2 == 0]
```

## Generator expressions are lazy

```python
squares = (number * number for number in range(1_000_000))
total = sum(squares)
```

The generator produces values as requested rather than building a list first. It is single-use and still performs the work when consumed. Laziness can reduce memory but does not make expensive computation free.

Functions often accept a generator expression without extra parentheses:

```python
total = sum(number * number for number in range(100))
```

## Avoid dense nesting

Multiple nested clauses and complicated conditions belong in named loops or helper functions. Compact is not automatically clear.

## Check your understanding

You are ready when you can translate between a loop and comprehension and choose a list or generator from reuse and memory needs.
