# Module 21: Translating Design to Python Control Flow

## Before you start

Complete Modules 01 to 20. You should understand variables, selection, loops, and how to run a small Python file.

## What you will learn

- assign variables and use basic types in Python
- read input and convert text to numbers
- write arithmetic expressions
- translate IF/ELSE designs into `if` / `elif` / `else`
- translate WHILE and FOR designs into `while` and `for`
- keep Python indentation aligned with design structure

## Why this matters

A design is only useful if you can implement it accurately. This module maps the control-flow ideas from ProgCon directly onto Python syntax.

## 1. Assignment and basic types

```python
name = "Ada"
score = 88
average = 91.5
passed = True
```

- text uses quotes: `"Ada"`
- whole numbers are integers: `88`
- numbers with fractional parts are floats: `91.5`
- booleans are `True` and `False` (capital T and F)

Assignment uses `=`. The right side is evaluated, then the result is stored in the name on the left.

## 2. Input and conversion

`input` always gives text (a string), even if the user types digits.

```python
raw_age = input("Enter age: ")
age = int(raw_age)
print(age)
```

Common converters:

- `int(...)` for whole numbers
- `float(...)` for decimal numbers

If the user types text that is not a number, conversion fails with `ValueError`. For this module, assume valid input unless an exercise asks you to handle a simple retry loop.

## 3. Arithmetic

```python
price = 50
discount = price * 0.10
total = price - discount
print(total)
```

Operators: `+`, `-`, `*`, `/`

Parentheses control order, just as in your designs.

## 4. Selection: if, elif, else

Pseudocode:

```text
IF score >= 75 THEN
    OUTPUT "Pass"
ELSE
    OUTPUT "Review"
END IF
```

Python:

```python
score = 80
if score >= 75:
    print("Pass")
else:
    print("Review")
```

Important Python rules:

- put a colon `:` at the end of `if`, `elif`, and `else` lines
- indent the body (four spaces is the course style)
- `elif` means "else if"

```python
score = 76
if score >= 90:
    print("Excellent")
elif score >= 75:
    print("Good progress")
elif score >= 60:
    print("Keep practicing")
else:
    print("Review the lesson")
```

## 5. Comparisons and logical operators

| Design idea | Python |
| --- | --- |
| equal to | `==` |
| not equal | `!=` |
| greater than | `>` |
| less than | `<` |
| greater or equal | `>=` |
| less or equal | `<=` |
| AND | `and` |
| OR | `or` |
| NOT | `not` |

```python
age = 20
has_id = True
if age >= 18 and has_id:
    print("Entry allowed")
```

Use `==` for comparison. A single `=` is assignment.

## 6. while loops

Pseudocode:

```text
SET count = 1
WHILE count <= 3
    OUTPUT count
    SET count = count + 1
END WHILE
```

Python:

```python
count = 1
while count <= 3:
    print(count)
    count = count + 1
```

The loop body must update the control variable, or the loop may never end.

## 7. for loops with range

A counted loop from 0 through 4:

```python
for index in range(5):
    print(index)
```

Output:

```text
0
1
2
3
4
```

`range(5)` produces `0,1,2,3,4`.

From 1 through 5 inclusive:

```python
for count in range(1, 6):
    print(count)
```

`range(start, stop)` stops before `stop`.

## 8. Full translation example

Design: input three scores, print average, print Pass if average >= 75.

```python
total = 0
for count in range(3):
    text = input("Enter score: ")
    score = float(text)
    total = total + score

average = total / 3
print("Average:", average)

if average >= 75:
    print("Pass")
else:
    print("Review")
```

Keep the design beside the code. Translate structure first, then fill syntax.

## Predict the result

```python
n = 2
if n > 5:
    print("Big")
else:
    print("Small")
```

Expected output: `Small`

## Common mistakes

### Using `=` inside a condition

Write `if score == 100:`, not `if score = 100:`.

### Forgetting the colon

`if`, `elif`, `else`, `while`, and `for` lines need `:`.

### Wrong indentation

Python uses indentation to mark the body of a decision or loop.

### Forgetting to convert input

`input` returns text. Convert before arithmetic.

### Off-by-one with range

`range(3)` gives three values: 0, 1, 2. It does not include 3.

## Check your understanding

1. Why do you often call `int` or `float` after `input`?
2. What is the difference between `=` and `==`?
3. How does Python show the body of an `if` statement?
4. What values does `range(4)` produce?
5. Translate `WHILE count < 10` into the first line of a Python while loop, assuming `count` already exists.

## Practice

Complete the [module exercises](./exercise/exercise.md). Then take the [module quiz](./quiz/quiz.md).

## Next step

In [Module 22](../22-translating-modules-and-arrays-to-python/README.md), you will implement modules as functions and arrays as lists.
