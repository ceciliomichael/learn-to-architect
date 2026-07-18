# Module 09: Lists and Mutation

## What you will learn

You will store ordered items, change lists deliberately, copy them, and avoid mutation surprises.

```python
colors = ["red", "green", "blue"]
print(colors[0])
print(colors[-1])
print(colors[1:])
```

Lists are ordered and mutable. Indexing and slicing follow string rules, but a slice creates a new list.

## Change contents

```python
colors[1] = "yellow"
colors.append("purple")
colors.insert(1, "orange")
removed = colors.pop()
```

`append` adds one object. `extend` visits an iterable and adds its items. `remove(value)` removes the first equal value and raises `ValueError` if absent. `pop(index)` removes and returns an item.

## Names can share one list

```python
first = [1, 2]
second = first
second.append(3)
print(first)  # [1, 2, 3]
```

Assignment did not copy the list. Both names refer to the same object. Make a shallow copy:

```python
second = first.copy()
```

A shallow copy creates a new outer list but shares nested mutable objects. Use `copy.deepcopy` only after understanding the data and whether independent nested objects are truly needed.

## Sort or create a sorted copy

```python
numbers = [3, 1, 2]
ordered = sorted(numbers)
numbers.sort()
```

`sorted` returns a new list. `list.sort` changes the list in place and returns `None`. Do not write `numbers = numbers.sort()`.

## Split and join text with lists

String `split` creates a list of text parts. String `join` combines an iterable of strings with a chosen separator:

```python
parts = "red,green,blue".split(",")
print(parts)
print(" | ".join(parts))
```

The separator belongs to `join`, so read the last line as joining the parts with ` | `. Every joined item must be a string.

## Do not change length while iterating

Removing items from the same list being visited can skip items. Build a new list with a loop:

```python
kept = []
for number in numbers:
    if number > 1:
        kept.append(number)
```

Module 16 introduces the compact comprehension form after this ordinary loop is clear.

## Check your understanding

You are ready when you can predict aliasing, choose mutation or a new list, explain shallow copies, and split text into a list.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
