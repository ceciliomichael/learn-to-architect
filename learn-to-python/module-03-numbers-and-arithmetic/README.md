# Module 03: Numbers and Arithmetic

## What you will learn

You will calculate with integers and floats and recognize when floating-point results are approximate.

## Numeric types

`int` stores whole numbers with arbitrary precision, limited by available memory. `float` normally uses double-precision binary floating point.

```python
items = 4
price = 2.5
print(type(items))
print(type(price))
```

## Arithmetic operators

```python
print(7 + 3)   # 10
print(7 - 3)   # 4
print(7 * 3)   # 21
print(7 / 3)   # true division, a float
print(7 // 3)  # floor division
print(7 % 3)   # remainder
print(7 ** 3)  # power
```

Floor division rounds toward negative infinity, not toward zero. Therefore `-7 // 3` is `-3`.

Use parentheses to state calculation order:

```python
subtotal = 20
tax_rate = 0.08
total = subtotal * (1 + tax_rate)
```

## Update a numeric name

```python
count = 5
count += 1
count *= 2
```

Augmented assignment rebinds an immutable number name to the calculated result.

## Floats are approximate

```python
print(0.1 + 0.2)
```

The result is not exactly 0.3 because many decimal fractions have no exact finite binary representation.

Do not compare important float calculations for exact equality without a tolerance. For measurements, `math.isclose` can express a tolerance. For exact base-10 rules such as some money calculations, use integer minor units or `decimal.Decimal` with a documented rounding policy. Module 32 teaches Decimal.

## Conversion and rounding

```python
print(int(3.9))       # 3, truncates toward zero
print(float(5))       # 5.0
print(round(2.675, 2))
```

`round` uses nearest with ties toward an even choice, but the stored float may not be the exact decimal you wrote. It is not a complete money policy.

## Division errors

Dividing by zero raises `ZeroDivisionError`. Do not hide it with an arbitrary result. Validate whether zero is allowed and choose domain behavior explicitly.

## Check your understanding

You are ready when you can choose `/`, `//`, or `%`, predict operator order, and explain why float display can be surprising.
