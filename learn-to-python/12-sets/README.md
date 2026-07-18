# Module 12: Sets and Membership

## What you will learn

You will store unique hashable values and use set operations for membership questions.

## A set stores unique values

```python
tags = {"python", "beginner", "python"}
print(tags)
```

The duplicate appears once. Sets are unordered collections; do not depend on printed order.

An empty set is:

```python
empty = set()
```

`{}` creates an empty dictionary.

## Change a set

```python
tags.add("practice")
tags.discard("missing")
tags.remove("beginner")
```

`discard` does nothing when absent. `remove` raises `KeyError`. Choose based on whether absence is normal.

Set members must be hashable. A set can contain strings and tuples of immutable hashable values, but not lists or dictionaries.

## Use set algebra

```python
required = {"read", "practice", "quiz"}
completed = {"read", "quiz"}

print(required | completed)  # union
print(required & completed)  # intersection
print(required - completed)  # difference
print(required ^ completed)  # symmetric difference
```

Relationship tests include:

```python
print(completed <= required)  # subset
print(required >= completed)  # superset
print(required.isdisjoint({"sleep"}))
```

## Remove duplicates with awareness

```python
names = ["Ava", "Ben", "Ava"]
unique_names = set(names)
```

This loses list order as a semantic guarantee. If first-seen order matters, use dictionary keys:

```python
unique_in_order = list(dict.fromkeys(names))
```

## Frozen sets

`frozenset` is an immutable set and can itself be a dictionary key or set member when its values are hashable:

```python
permissions = frozenset({"read", "write"})
```

## Sets and performance

Set membership is usually fast because of hashing, but do not make exact timing claims without measurement. Hash collisions, object behavior, and input size still matter.

## Common mistakes

- Writing `{}` for an empty set.
- Depending on set order.
- Putting a list in a set.
- Using set conversion when duplicate counts or order matter.

## Check your understanding

You are ready when you can choose union, intersection, or difference and explain hashability and order loss.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
