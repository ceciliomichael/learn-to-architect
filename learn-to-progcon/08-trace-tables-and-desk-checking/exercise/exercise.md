# Module 08 Exercises

## Warm-up: Complete a small trace

Design:

```text
BEGIN
  INPUT a
  INPUT b
  SET total = a + b
  SET doubleTotal = total * 2
  DISPLAY doubleTotal
END
```

Sample inputs: `a = 4`, `b = 6`.

1. Create a trace table with columns for `a`, `b`, `total`, `doubleTotal`, and Output.
2. Fill one row per instruction after START.
3. State the final displayed value.
4. State the expected value and confirm they match.

## Guided exercise: Trace a discount design

Design:

```text
BEGIN
  CONSTANT RATE = 0.10
  INPUT price
  SET discount = price * RATE
  SET finalPrice = price - discount
  DISPLAY finalPrice
END
```

1. Predict the final price for `price = 80` before filling a full table.
2. Build a complete trace table for that sample.
3. Mark which row first creates `discount` and which row first creates `finalPrice`.
4. Change the sample to `price = 50` and make a second short table or row set for the final few computed values.
5. Explain why two samples are more convincing than one for a rate formula.

## Independent exercise: Build, trace, and verify

Problem: Read three daily temperatures (Celsius). Compute their average. Display the average.

Requirements:

1. Write sequential pseudocode.
2. Choose sample temperatures with an easy expected average. State that expected average first.
3. Build a full trace table for your design with those samples.
4. Confirm the Output column matches your expected average.
5. Write one sentence about which intermediate column (`sum` or similar) helps you trust the final average.

Your variable names may differ, but the table columns must match the names in your pseudocode.

## Debugging / desk-check task

Broken design for "pay = hours * rate, then display pay":

```text
BEGIN
  SET pay = hours * rate
  INPUT hours
  INPUT rate
  DISPLAY pay
END
```

Sample intended inputs: `hours = 8`, `rate = 15`. Expected pay: `120`.

Tasks:

1. Attempt a trace table and explain where it breaks or becomes undefined.
2. Identify the design defect (order and missing update).
3. Write a corrected design.
4. Provide a complete correct trace table for the sample.
5. Choose one extra sample (for example `hours = 0`, `rate = 15`) and state what the corrected design should display. Briefly say why that sample is useful.

## Completion checklist

- [ ] I can build columns for each variable and for output.
- [ ] I update a trace table row by row.
- [ ] I compare table results with an expected value chosen in advance.
- [ ] I can spot wrong formulas and wrong order in a table.
- [ ] I can choose sample values that make mistakes visible.

Compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md) after attempting every task.
