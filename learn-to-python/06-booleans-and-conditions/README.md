# Module 06: Booleans and Conditions

## What you will learn

You will create boolean conditions and choose exactly one path with `if`, `elif`, and `else`.

## Comparisons produce bool

```python
age = 20
print(age >= 18)
print(age == 20)
print(age != 10)
```

Use `==` for equality and `=` for assignment. Chained comparisons are valid:

```python
print(0 <= age < 130)
```

## Choose a path

```python
temperature = 28

if temperature >= 30:
    print("Hot")
elif temperature >= 20:
    print("Comfortable")
else:
    print("Cool")
```

The colon begins a block. Four spaces indent its statements. Python checks branches from top to bottom and runs the first true branch.

## Combine conditions

```python
has_ticket = True
age = 16

if has_ticket and age >= 13:
    print("Entry allowed")
```

- `and` requires both sides to be truthy.
- `or` requires at least one.
- `not` reverses truth.

`not` is evaluated before `and`, and `and` before `or`. Use parentheses when mixing them.

## Membership and identity

```python
course = "Python foundations"
print("Python" in course)

note = None
print(note is None)
```

For text, `in` checks whether one string occurs inside another. Later collection modules use the same operator for stored items. Use `==` for value equality and `is` mainly for singleton identity such as `None`. Do not use `is` to compare ordinary numbers or strings.

## Truthy and falsy objects

`False`, `None`, numeric zero, and an empty string are falsy. Collection modules later show that empty collections are also falsy. Most other objects are truthy.

```python
name = input("Name: ").strip()
if name:
    print(f"Hello, {name}")
else:
    print("A name is required.")
```

Explicit comparisons can be clearer when zero and missing have different meanings.

## Short-circuit behavior

Python stops once the whole result is known:

```python
denominator = 0
if denominator != 0 and 10 / denominator > 2:
    print("Large result")
```

The division is not evaluated when the first condition is false.

## Check your understanding

You are ready when you can order branches from specific to general and choose equality, membership, or identity correctly.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
