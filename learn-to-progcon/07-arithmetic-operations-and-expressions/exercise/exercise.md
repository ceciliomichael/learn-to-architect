# Module 07 Exercises

## Warm-up: Evaluate expressions

Compute each result using standard order of operations. Show a short middle step when useful.

1. `5 + 4 * 2`
2. `(5 + 4) * 2`
3. `18 / 3 * 2`
4. `18 / (3 * 2)`
5. `100 - 20 - 10`
6. `100 - (20 - 10)`

## Guided exercise: Grade average with clear formulas

Problem: Read three quiz scores and display their average.

1. Write sequential pseudocode that:
   - inputs `score1`, `score2`, and `score3`
   - computes `sum`
   - computes `average` with a correct formula
   - displays `average`
2. Explain why parentheses are needed if you write the average as one expression without a separate `sum`.
3. Desk-check with scores `70`, `85`, and `90`. Show `sum` and `average`.
4. State what would go wrong if the design used `SET average = score1 + score2 + score3 / 3`.

Expected average for the sample: `81.666...` (or an exact fraction `245/3` if you keep it as a fraction). A decimal around `81.67` is fine if you show your division clearly.

## Independent exercise: Discount and tax receipt

Problem: A shop offers 25 percent off, then adds 8 percent tax on the discounted price.

Requirements:

1. Use constants for the discount rate and tax rate.
2. Input an `originalPrice`.
3. Compute:
   - discount amount
   - discounted price
   - tax amount
   - amount due
4. Display the amount due.
5. Keep units as money amounts (numbers). Use rates as decimals.
6. Desk-check with `originalPrice = 120` and show each intermediate value.
7. Write the design so each assignment is a complete instruction with a clear expression on the right side.

Do not apply tax before the discount. Follow the stated order.

## Debugging / desk-check task

A learner wrote this design for "average of two temperatures, then convert that average from Celsius to Fahrenheit."

Broken design:

```text
BEGIN
  INPUT temp1
  INPUT temp2
  SET averageC = temp1 + temp2 / 2
  SET averageF = averageC * 9 / 5 + 32
  DISPLAY averageF
END
```

Sample intended inputs: `temp1 = 10`, `temp2 = 20`.

The intended Celsius average is `15`. The intended Fahrenheit result uses the normal conversion on that average.

Tasks:

1. Identify the formula mistakes (there may be more than one issue to discuss: grouping and clarity).
2. State what the broken design actually computes for the sample inputs.
3. Write a corrected design.
4. Desk-check the corrected design for the sample inputs and give the final displayed Fahrenheit value.

## Completion checklist

- [ ] I can evaluate `+ - * /` with parentheses and default order.
- [ ] I can write complete assignment instructions, not floating expressions alone.
- [ ] I can design totals, averages, discounts, and tax formulas.
- [ ] I keep rates as decimals when multiplying.
- [ ] I can find wrong grouping in a desk-check.

Compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md) after attempting every task.
