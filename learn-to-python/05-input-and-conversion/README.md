# Module 05: Input and Conversion

## What you will learn

You will read terminal input, convert text to numbers, and understand conversion errors.

## input always returns text

```python
name = input("What is your name? ")
print(f"Hello, {name}!")
```

The prompt should state what the user needs to enter. The returned object is a string, even when the user types digits.

```python
age_text = input("Age in whole years: ")
print(type(age_text))
```

## Convert deliberately

```python
age = int(age_text)
height = float(input("Height in meters: "))
```

`int` accepts valid whole-number text such as `"42"` or `"-7"`. `float` accepts forms such as `"1.75"`. Surrounding whitespace is accepted by these conversions.

Invalid text raises `ValueError`. Do not pretend that `"ten"` is zero. Conditions and loops are taught next, and exception handling comes later. For now, read the traceback, rerun, and enter the requested form.

## Convert before arithmetic

```python
quantity = int(input("Quantity: "))
unit_price = float(input("Unit price: "))
subtotal = quantity * unit_price
print(f"Subtotal: {subtotal:.2f}")
```

Without conversion, multiplying a string by an integer repeats text, and adding two input strings concatenates them.

## Conversion can lose information

```python
print(int(3.9))
print(str(42))
```

`int(3.9)` truncates toward zero. It does not round. `str` creates display text. Choose conversion from the meaning, not merely to silence an error.

## Never use eval for input

`eval(input())` can execute arbitrary Python code. It is not a shortcut for numeric input. Use a specific conversion and validate allowed ranges once control flow is available.

## Check your understanding

You are ready when you can explain why input is text, convert valid numeric input, and recognize `ValueError` without inventing a fallback.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
