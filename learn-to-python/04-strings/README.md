# Module 04: Text and String Operations

## What you will learn

You will create Unicode text, index and slice it, call methods, and format readable output.

## Strings contain text

```python
title = "Python Basics"
message = 'Welcome'
```

Both quote styles create `str` objects. Use escapes or a different outer quote:

```python
print("It's ready.")
print("First line\nSecond line")
```

Python strings are Unicode text. Bytes are a separate type used for encoded data and files.

## Length, indexing, and slicing

```python
word = "Python"
print(len(word))  # 6
print(word[0])    # P
print(word[-1])   # n
print(word[1:4])  # yth
print(word[:2])   # Py
print(word[2:])   # thon
```

Indexes begin at 0. A slice includes its start and excludes its stop. An out-of-range index raises `IndexError`; a slice safely stops at the available boundary.

## Strings are immutable

This fails:

```python
word[0] = "J"
```

Methods create new strings:

```python
raw_name = "  Mira Chen  "
clean_name = raw_name.strip()
print(clean_name.upper())
print(raw_name)
```

Useful methods include `lower`, `upper`, `strip`, `replace`, `startswith`, `endswith`, and `find`.

```python
status = "not ready".replace("not ready", "ready")
print(status)
```

Splitting text creates a list, so `split` and `join` are introduced after lists in Module 09.

## Format with f-strings

```python
name = "Ava"
score = 9
print(f"{name} scored {score} points.")
```

An expression inside braces is evaluated:

```python
price = 12.5
print(f"Price: {price:.2f}")
```

Formatting does not make a float exact. It controls display.

Do not place untrusted text inside the source of an f-string and evaluate it. Use values inside a fixed f-string.

## Search and membership

```python
print("SQL" in "Python and SQL")
print("python" in "Python")
```

Membership is case-sensitive. Simple lowercase comparison is useful for basic ASCII cases, but international case-insensitive matching can require `casefold` and domain rules.

## Common mistakes

- Confusing index 1 with the first character.
- Expecting methods to mutate the original string.
- Using `+` between text and a number instead of conversion or an f-string.
- Treating displayed decimal digits as exact numeric storage.

## Check your understanding

You are ready when you can predict slices, create a cleaned copy, and format values without changing their stored objects.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
