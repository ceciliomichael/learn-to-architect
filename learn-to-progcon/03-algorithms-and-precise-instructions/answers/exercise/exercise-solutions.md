# Module 03 Exercise Solutions

Your wording can differ if the algorithm stays ordered, precise, and finite, and if the hand-check results match.

## Warm-up solution

```text
1. Input price.
2. Input quantity.
3. Set subtotal to price * quantity.
4. Output subtotal.
5. Stop.
```

Hand-check: price `4`, quantity `5`

- subtotal = 4 * 5 = 20
- expected output: `20`

## Guided exercise solution

### 1. Inputs

score1, score2, score3

### 2. Possible outputs

`"Ready for next unit"` or `"Needs practice"`

### 3. Algorithm

```text
1. Input score1.
2. Input score2.
3. Input score3.
4. Set sum to score1 + score2 + score3.
5. Set average to sum / 3.
6. If average is greater than or equal to 70, output "Ready for next unit".
7. Otherwise, output "Needs practice".
8. Stop.
```

### 4. Hand-check: 60, 70, 80

- sum = 210
- average = 70
- average >= 70 is true
- message: `Ready for next unit`

### 5. Hand-check: 50, 55, 60

- sum = 165
- average = 55
- average >= 70 is false
- message: `Needs practice`

## Independent exercise solution

### Algorithm A

```text
1. Input celsius.
2. Set fahrenheit to (celsius * 9 / 5) + 32.
3. Output fahrenheit.
4. Stop.
```

### Algorithm B

```text
1. Input orderTotal.
2. If orderTotal is greater than or equal to 40, set shipping to 0.
3. Otherwise, set shipping to 6.
4. Output shipping.
5. Stop.
```

### Hand-check A: celsius 10

- fahrenheit = (10 * 9 / 5) + 32 = 18 + 32 = 50
- expected output: `50`

### Hand-check B

- orderTotal `40`: shipping `0`
- orderTotal `39.99`: shipping `6`

### Why precision matters for "40"

"Around 40" is vague. Two people might treat `39.99`, `40`, and `40.01` differently. "Greater than or equal to 40" makes the boundary exact, so tests and later programs can agree.

## Debugging / desk-check task solution

### 1. Problems

Examples of valid issues:

1. "quantity is big" is not precise. It does not say at least 5.
2. "make it cheaper" does not say 10% off or how to compute it.
3. "Show something" does not name the output value.
4. There is no clear stop, so the finite end is not stated.
5. The algorithm is hard to test because expected results cannot be fixed from the vague words.
6. Value names are incomplete after the inputs (total is used without a clear update rule for the discount).

### 2. Corrected algorithm

```text
1. Input price.
2. Input quantity.
3. Set total to price * quantity.
4. If quantity is greater than or equal to 5, set total to total * 0.90.
5. Output total.
6. Stop.
```

### 3. Desk-check: price 3, quantity 5

- total = 15
- quantity >= 5 is true, so total = 15 * 0.90 = 13.5
- expected output: `13.5`

### 4. Desk-check: price 3, quantity 4

- total = 12
- quantity >= 5 is false, so total stays 12
- expected output: `12`
