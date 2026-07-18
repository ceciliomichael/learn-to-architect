# Module 11: Dictionaries

## What you will learn

You will model named fields, look up values, update mappings safely, and iterate over keys and values.

## A dictionary maps keys to values

```python
book = {
    "title": "First Steps",
    "author": "Mira Chen",
    "year": 2026,
}

print(book["title"])
```

Keys are unique and must be hashable. Strings, numbers, and tuples of hashable values can be keys. Lists and dictionaries cannot be keys because their contents can change.

Values can be any Python object.

## Add and update entries

```python
book["in_stock"] = True
book["year"] = 2027
```

Assignment adds a missing key or replaces the value for an existing key.

Delete deliberately:

```python
removed = book.pop("in_stock")
```

`del book["year"]` also removes an entry but returns no value.

## Handle missing keys by meaning

```python
print(book.get("subtitle"))
print(book.get("subtitle", "No subtitle"))
```

`get` returns `None` or a chosen default when the key is absent. Bracket lookup raises `KeyError`, which is useful when the key is required and absence is a bug.

Do not use a default that hides invalid data. Required fields should be validated.

## Test keys and iterate

```python
if "author" in book:
    print(book["author"])

for key in book:
    print(key)

for key, value in book.items():
    print(key, value)
```

Iteration over a dictionary visits keys. `values()` visits values and `items()` visits key-value pairs.

Dictionaries preserve insertion order in Python 3.7 and newer. Equality depends on key-value content, not insertion order. Sort explicitly when output order has a separate requirement.

## Copying and nesting

```python
copy_of_book = book.copy()
```

This is shallow. Nested lists or dictionaries remain shared.

```python
course = {
    "title": "Python",
    "lessons": ["values", "conditions"],
}
```

Read one level at a time and validate external shapes before nested lookup.

## Merge mappings consciously

```python
defaults = {"theme": "light", "page_size": 20}
user = {"page_size": 50}
settings = defaults | user
```

On duplicate keys, the right mapping wins. The `|` operator requires Python 3.9 or newer and creates a new dictionary.

## Common mistakes

- Expecting `in` to search values instead of keys.
- Using `get` for a required field and letting `None` travel unnoticed.
- Modifying dictionary size during iteration.
- Assuming shallow copy duplicates nested objects.

## Check your understanding

You are ready when you can choose bracket access or `get`, iterate through pairs, and explain key hashability.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
