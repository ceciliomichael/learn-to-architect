# Module 07: Arithmetic Operations and Expressions

## Before you start

Complete Modules 01 to 06. You should be able to:

- write sequential pseudocode with named storage
- use assignment with right-side evaluation first
- choose clear variable and constant names
- keep conceptual types straight (text, number, yes/no)

## What you will learn

- the basic arithmetic operators: `+`, `-`, `*`, `/`
- parentheses and order of operations
- the difference between an expression and a complete instruction
- integer division versus real (decimal) division at a concept level
- formulas for totals, averages, discounts, and tax
- how to keep units clear so results stay meaningful

## Why this matters

Many programs exist to calculate something: a bill, a grade average, a discount price, a temperature conversion. If the formula is wrong, the whole solution is wrong even when the flowchart looks tidy. Careful arithmetic design is a core programming skill.

## 1. The four basic operators

In design work, these symbols are standard:

| Operator | Meaning | Example | Result idea |
| --- | --- | --- | --- |
| `+` | add | `3 + 4` | 7 |
| `-` | subtract | `10 - 3` | 7 |
| `*` | multiply | `5 * 2` | 10 |
| `/` | divide | `20 / 4` | 5 |

Everyday examples:

```text
SET total = price1 + price2
SET change = paid - total
SET lineTotal = unitPrice * quantity
SET average = sum / count
```

Use `*` for multiplication in designs and code-style pseudocode. Do not write `x` or `·` unless your teacher or team has an agreed paper style. This course uses `*`.

## 2. Expressions versus complete instructions

An expression is a piece of design language that produces a value.

Examples of expressions:

- `3 + 4`
- `price * quantity`
- `(score1 + score2) / 2`
- `originalPrice * DISCOUNT_RATE`

A complete instruction tells the solution to do something with that value, such as store it or display it.

Examples of complete instructions:

```text
SET total = price * quantity
DISPLAY average
INPUT count
```

This line is an expression only, not a full step by itself:

```text
price * quantity
```

This line is a complete assignment instruction that uses the expression:

```text
SET lineTotal = price * quantity
```

When you write algorithms, prefer complete instructions. Expressions appear on the right side of assignment, inside displays, or inside later conditions.

## 3. Order of operations

When an expression has more than one operator, evaluation order matters.

Common order used in this course (and in most programming languages):

1. Evaluate expressions inside parentheses first, from inner to outer.
2. Then multiply and divide from left to right.
3. Then add and subtract from left to right.

### Example A

```text
SET result = 2 + 3 * 4
```

Multiplication happens before addition:

- `3 * 4` is 12
- `2 + 12` is 14
- `result` is 14

Not 20. The design does not mean `(2 + 3) * 4` unless you write the parentheses.

### Example B

```text
SET result = (2 + 3) * 4
```

Parentheses first:

- `2 + 3` is 5
- `5 * 4` is 20
- `result` is 20

### Example C

```text
SET result = 20 / 2 * 5
```

Multiply and divide are the same priority, so go left to right:

- `20 / 2` is 10
- `10 * 5` is 50
- `result` is 50

### Predict the result

```text
SET a = 10 - 4 - 2
SET b = 10 - (4 - 2)
```

What are `a` and `b`?

- `a`: left to right, `10 - 4` is 6, then `6 - 2` is 4
- `b`: parentheses first, `4 - 2` is 2, then `10 - 2` is 8

Final: `a` is 4, `b` is 8.

When a formula is important, use parentheses even if you think the default order already works. Parentheses make intent obvious to human readers.

## 4. Parentheses for clarity and correctness

Two reasons to use parentheses:

1. **Correctness:** force a non-default order.
2. **Clarity:** show the intended grouping even when default order is already correct.

Average of two scores:

```text
SET average = (score1 + score2) / 2
```

Without parentheses:

```text
SET average = score1 + score2 / 2
```

That second form is usually wrong for an average. It divides only `score2` by 2, then adds `score1`.

Tax then total:

```text
SET tax = price * TAX_RATE
SET total = price + tax
```

Or in one carefully grouped expression:

```text
SET total = price + (price * TAX_RATE)
```

Both can work. Two shorter steps are often easier to desk-check.

## 5. Integer division versus real division (concept)

Division can produce different kinds of results depending on the language and the types of values. At the design stage, you must decide what kind of answer the problem needs.

### Real division (decimal result allowed)

Real division keeps a fractional part when needed.

Examples:

- `7 / 2` is `3.5`
- `5 / 2` is `2.5`
- `10 / 4` is `2.5`

Use real division for money averages, grade averages, rates, and most measurements.

### Integer division (whole-number focus)

Integer division focuses on whole numbers. The exact rule depends on the later language, but the concept is:

- you are interested in how many whole groups fit, or
- you intentionally drop or separate the fractional part

Example everyday idea:

- 7 apples shared into bags of 2
- whole full bags: 3
- leftover apples: 1

So:

- whole-groups idea: `7` divided by `2` gives `3` full groups
- remainder idea: `1` left over

In pure design, write what you mean in words if the problem needs whole groups:

```text
SET fullBoxes = numberOfItems / itemsPerBox   // intend whole boxes only
SET leftover = numberOfItems - (fullBoxes * itemsPerBox)
```

Or state the rule in a comment:

```text
// Use whole-number division: discard the fraction for this packing problem
```

### Why this matters

If a student average should be `85.5`, integer-style chopping to `85` may hide the true result. If a factory packs whole boxes only, a fractional box may be the wrong model.

In this course, unless a problem says it needs whole groups only, prefer real division that keeps decimals when they appear.

## 6. Totals

A total combines amounts with addition, or combines unit price and quantity with multiplication.

### Sum of several values

```text
SET total = item1 + item2 + item3
```

### Price times quantity

```text
SET total = unitPrice * quantity
```

### Running total pattern

```text
SET total = 0
SET total = total + item1
SET total = total + item2
SET total = total + item3
```

All three forms are common. Choose the form that matches the problem and the order of inputs.

### Predict the result

```text
SET unitPrice = 12
SET quantity = 3
SET total = unitPrice * quantity
```

`total` becomes `36`.

## 7. Averages

An average (mean) is the sum of values divided by the count of values.

```text
SET sum = score1 + score2 + score3
SET average = sum / 3
```

Or:

```text
SET average = (score1 + score2 + score3) / 3
```

Keep the parentheses when the sum and the division share one expression.

### Count must match the values you included

If you average four scores, divide by 4, not by 3. A frequent logic bug is summing four numbers and dividing by the wrong count.

### Predict the result

Scores: 70, 80, 90

```text
SET sum = 70 + 80 + 90
SET average = sum / 3
```

`sum` is 240. `average` is 80.

## 8. Discounts

A discount reduces a price.

Common pieces:

- original price
- discount rate (such as 0.15 for 15 percent)
- discount amount
- final price

Example:

```text
CONSTANT DISCOUNT_RATE = 0.15
SET originalPrice = 200
SET discountAmount = originalPrice * DISCOUNT_RATE
SET finalPrice = originalPrice - discountAmount
```

Walk-through:

- discount amount: `200 * 0.15 = 30`
- final price: `200 - 30 = 170`

Percent reminder:

- 15 percent as a rate is `0.15`
- 8 percent as a rate is `0.08`
- 100 percent as a rate is `1.0`

If a problem gives "20% off," convert to rate `0.20` before multiplying.

One-line form:

```text
SET finalPrice = originalPrice * (1 - DISCOUNT_RATE)
```

With rate `0.15`:

- `1 - 0.15 = 0.85`
- `200 * 0.85 = 170`

Same result. The multi-step form is often easier for beginners to check.

## 9. Tax

Tax adds a charge based on a rate.

```text
CONSTANT TAX_RATE = 0.08
SET price = 50
SET tax = price * TAX_RATE
SET totalDue = price + tax
```

Walk-through:

- tax: `50 * 0.08 = 4`
- total due: `50 + 4 = 54`

Discount then tax, or tax then discount, can differ depending on business rules. Always follow the problem statement order. Do not invent a legal tax rule. Implement the rule the problem gives.

Example required order: apply discount first, then tax on the discounted price.

```text
CONSTANT DISCOUNT_RATE = 0.10
CONSTANT TAX_RATE = 0.08
SET originalPrice = 100
SET discountedPrice = originalPrice * (1 - DISCOUNT_RATE)
SET tax = discountedPrice * TAX_RATE
SET totalDue = discountedPrice + tax
```

Walk-through:

- discounted price: `100 * 0.90 = 90`
- tax: `90 * 0.08 = 7.2`
- total due: `90 + 7.2 = 97.2`

## 10. Keep units clear

A unit tells what a number measures: pesos, points, degrees Celsius, seats, minutes, kilograms.

Good designs keep units consistent inside each formula.

### Compatible units

```text
SET totalMinutes = hours * 60 + minutes
```

Here hours are converted to minutes before adding minutes.

### Incompatible mix without conversion

Broken idea:

```text
SET total = hours + minutes
```

If `hours` is 2 and `minutes` is 30, `total` as `32` is not meaningful as either pure hours or pure minutes without a rule.

### Label results in messages when helpful

```text
DISPLAY "Average score:"
DISPLAY average
```

Or in one message design note:

```text
DISPLAY average   // points out of 100
```

### Money and decimals

Money calculations often need decimal results. Keep rates and prices as numbers that can hold fractional parts when the problem needs them. Rounding rules (to two decimal places, for example) are a later implementation detail unless the problem states a rounding rule now. If the problem does not require rounding, compute the exact design value and state it clearly.

### Temperature units

```text
SET fahrenheit = (celsius * 9 / 5) + 32
```

The formula assumes `celsius` is in degrees Celsius and produces degrees Fahrenheit. Do not feed Fahrenheit into a Celsius-only formula without converting.

## 11. Full worked design: shop receipt

Problem: A customer buys one item. Read the unit price and quantity. Apply a 10 percent discount. Then add 5 percent tax on the discounted amount. Display the final amount due.

```text
BEGIN
  CONSTANT DISCOUNT_RATE = 0.10
  CONSTANT TAX_RATE = 0.05
  DISPLAY "Enter unit price"
  INPUT unitPrice
  DISPLAY "Enter quantity"
  INPUT quantity
  SET gross = unitPrice * quantity
  SET discountAmount = gross * DISCOUNT_RATE
  SET discounted = gross - discountAmount
  SET tax = discounted * TAX_RATE
  SET amountDue = discounted + tax
  DISPLAY amountDue
END
```

Sample values: unit price `40`, quantity `2`.

| Step | Important values |
| --- | --- |
| after inputs | unitPrice 40, quantity 2 |
| gross | 80 |
| discountAmount | 8 |
| discounted | 72 |
| tax | 3.6 |
| amountDue | 75.6 |

Displayed result: `75.6`

This design uses short complete instructions. Each expression is small enough to check.

## 12. Writing formulas that other people can verify

Checklist for arithmetic steps:

1. Are all names set before the formula uses them?
2. Does operator order match the intended math?
3. Do parentheses show the intended grouping?
4. Is the count in an average equal to the number of values summed?
5. Are rates written as decimals when multiplying (`0.15`, not `15`, unless you also divide by 100)?
6. Are units consistent?
7. Is each line a complete instruction, not a floating expression with no store or display?

If you cannot desk-check a formula with one sample, simplify the steps.

## Common mistakes

1. **Forgetting parentheses in averages**  
   `score1 + score2 / 2` is not the average of two scores.

2. **Using percent numbers without converting to rates**  
   `price * 15` is not 15 percent off. Use `0.15`, or use `15 / 100`.

3. **Wrong divisor in averages**  
   Summing three scores and dividing by 2 produces a false average.

4. **Treating an expression as a full step**  
   Write `SET total = a + b`, not only `a + b`, unless your notation clearly implies assignment.

5. **Mixing units**  
   Adding hours to minutes without conversion creates a meaningless number.

6. **Assuming integer chopping when decimals matter**  
   Grade and money averages often need fractional results.

7. **Hiding too much in one giant expression**  
   Long formulas are harder to check. Prefer clear intermediate names when learning.

## Check your understanding

1. What is the value of `2 + 6 * 3` using standard order of operations?
2. Why are parentheses required in `(score1 + score2) / 2` for an average?
3. What is the difference between an expression and a complete instruction?
4. Compute a 20 percent discount on price `80`. What is the final price after the discount (before any tax)?
5. Why is `hours + minutes` risky without conversion?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

Module 08 teaches trace tables and desk checking. You will track every variable step by step and catch wrong formulas before coding.
