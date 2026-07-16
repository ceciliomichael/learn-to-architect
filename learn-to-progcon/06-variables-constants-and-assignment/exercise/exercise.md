# Module 06 Exercises

## Warm-up: Name the storage

For each piece of information, choose a clear name and say whether it should be a variable or a constant in a typical design. Also state the conceptual type (text, number, or yes/no).

1. A shopper's first name entered at checkout
2. A fixed sales tax rate of 0.08 used for every item in this problem
3. A running total of purchases that grows as items are scanned
4. Whether a student is marked present (`true` or `false`)
5. The room capacity limit of 25 seats for an event

## Guided exercise: Build a small assignment design

Write sequential pseudocode for this problem:

- Ask for the price of a notebook.
- Ask for the price of a pen.
- Store each price in a clearly named variable.
- Compute `total` as the sum of the two prices.
- Display `total`.

Then complete these steps:

1. List every variable name and its conceptual type.
2. Mark which lines introduce a name and which lines only use a name.
3. Desk-check with notebook price `45` and pen price `12`. Write the value of each variable after each assignment.
4. Draw a short sequence flowchart that matches your pseudocode names exactly.

Expected final total for the sample: `57`.

## Independent exercise: Temperature setup and conversion names

Problem: Convert a Celsius temperature to Fahrenheit with named storage.

Requirements:

1. Use an input variable for Celsius (choose a clear name).
2. Use a variable for the Fahrenheit result.
3. Use this formula idea: Fahrenheit equals Celsius times 9 divided by 5, then plus 32.
4. Write full sequential pseudocode with `BEGIN` and `END`.
5. Include at least one constant if you introduce fixed numbers as named constants (optional but preferred for `32` or similar fixed parts only if it improves clarity; you may keep `9`, `5`, and `32` in the formula if you document the formula clearly).
6. Desk-check with Celsius input `10` and state the Fahrenheit result.
7. State the conceptual type of each name you used.

Your design must set every name before it is used in a later calculation or display.

## Debugging / desk-check task

Find and correct every problem in this design. Then desk-check the corrected version with the sample inputs shown in the comments.

Broken design:

```text
BEGIN
  SET total = price + tax
  DISPLAY "Enter price"
  INPUT price
  CONSTANT taxRate = 0.1
  SET tax = price * taxRate
  SET price = "cheap"
  DISPLAY total
END
```

Sample intended inputs:

- numeric price `50`
- tax rate constant `0.1`

What the design should do:

- read a numeric price
- compute tax as price times 0.1
- compute total as price plus tax
- display total

Tasks:

1. List each bug (order errors, type confusion, misuse of names, or missing assignment updates).
2. Write a corrected pseudocode design.
3. Desk-check the corrected design with price `50`. Show `tax` and `total`.

## Completion checklist

- [ ] I can choose clear names without spaces.
- [ ] I can tell variables from constants for a simple problem.
- [ ] I evaluate the right side of assignment before storing on the left.
- [ ] I set names before I use them.
- [ ] I keep conceptual types consistent with the operations.

Compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md) after attempting every task.
