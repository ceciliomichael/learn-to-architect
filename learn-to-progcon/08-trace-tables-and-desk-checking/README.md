# Module 08: Trace Tables and Desk Checking

## Before you start

Complete Modules 01 to 07. You should be able to:

- write sequential pseudocode with clear names
- use assignment and arithmetic expressions correctly
- draw a basic sequence flowchart
- walk a short design with sample values by hand

## What you will learn

- what a trace table is and why designers use one
- how to build columns for each variable and for output
- how to update a table row by row as each instruction runs
- how desk checking finds mistakes before coding
- how wrong formulas and wrong order show up in a trace
- how to choose sample values that reveal bugs

## Why this matters

A design can look neat and still be wrong. Desk checking is the habit of following your own instructions carefully with real sample data. A trace table turns that habit into a clear written record. You catch errors while changes are still cheap: before typing a full program.

## 1. What desk checking is

Desk checking means you execute a design by hand. You play the role of the computer. You read each instruction in order, update stored values, and record outputs.

Desk checking helps you answer:

- Does this plan use names before they are set?
- Does the formula produce the intended result?
- Is the step order correct?
- Does the output match what the problem asks for?

Desk checking does not replace later software testing. It reduces obvious logic mistakes early. After coding (later in the course), you still run the program with tests. Design checks and run-time checks work together.

## 2. What a trace table is

A trace table is a chart that records the value of each important name after selected steps. It may also record output.

Typical columns:

- Step (or line / instruction summary)
- one column per variable
- one column per constant if you want to show it (optional)
- Output (optional but very useful)

Each new row shows what changed after the next instruction.

Simple idea:

```text
Instruction order --> down the rows
Variable names    --> across the columns
```

You are building a history of the solution's memory.

## 3. Build the columns first

Start from the design. List every name that stores a value.

Example design:

```text
BEGIN
  INPUT price
  INPUT quantity
  SET total = price * quantity
  DISPLAY total
END
```

Useful columns:

| Step | price | quantity | total | Output |
| --- | --- | --- | --- | --- |

Tips:

- Include every variable that is assigned or input.
- Include output when the design displays something.
- You may omit pure constants if they never change and clutter the table. Keep them if they help the check.
- Keep column names identical to design names.

## 4. Update row by row

Choose sample inputs. Then execute one instruction at a time.

Sample inputs: `price = 15`, `quantity = 3`.

| Step | price | quantity | total | Output |
| --- | --- | --- | --- | --- |
| INPUT price | 15 |  |  |  |
| INPUT quantity | 15 | 3 |  |  |
| SET total = price * quantity | 15 | 3 | 45 |  |
| DISPLAY total | 15 | 3 | 45 | 45 |

Reading rules:

1. Copy forward values that did not change, or leave them blank if your classroom style only writes changes. This course prefers filling the current known values so each row is easy to read alone.
2. Evaluate the right side with the values from the current memory state.
3. Write the new left-side value in that row.
4. When a display happens, write the displayed value in the Output column.

At the end, compare the output with the expected result for the sample. Here the expected total is `15 * 3 = 45`. The table matches, so this design passes this sample.

## 5. A fuller example: average of three scores

Design:

```text
BEGIN
  INPUT score1
  INPUT score2
  INPUT score3
  SET sum = score1 + score2 + score3
  SET average = sum / 3
  DISPLAY average
END
```

Sample inputs: 70, 80, 90. Expected average: 80.

| Step | score1 | score2 | score3 | sum | average | Output |
| --- | --- | --- | --- | --- | --- | --- |
| INPUT score1 | 70 |  |  |  |  |  |
| INPUT score2 | 70 | 80 |  |  |  |  |
| INPUT score3 | 70 | 80 | 90 |  |  |  |
| SET sum = ... | 70 | 80 | 90 | 240 |  |  |
| SET average = ... | 70 | 80 | 90 | 240 | 80 |  |
| DISPLAY average | 70 | 80 | 90 | 240 | 80 | 80 |

The table confirms both intermediate and final values. If `sum` were wrong, you would see it before trusting `average`.

## 6. Finding wrong formulas with a trace

Broken design:

```text
BEGIN
  INPUT score1
  INPUT score2
  SET average = score1 + score2 / 2
  DISPLAY average
END
```

Sample inputs: 10 and 20. Intended average: 15.

Trace of the broken design:

| Step | score1 | score2 | average | Output |
| --- | --- | --- | --- | --- |
| INPUT score1 | 10 |  |  |  |
| INPUT score2 | 10 | 20 |  |  |
| SET average = score1 + score2 / 2 | 10 | 20 | 20 |  |
| DISPLAY average | 10 | 20 | 20 | 20 |

Why `average` became 20:

- `score2 / 2` is 10
- `score1 + 10` is 20

Expected was 15. The trace proves the formula is wrong for this sample. Fix:

```text
SET average = (score1 + score2) / 2
```

New trace:

| Step | score1 | score2 | average | Output |
| --- | --- | --- | --- | --- |
| inputs done | 10 | 20 |  |  |
| SET average = (score1 + score2) / 2 | 10 | 20 | 15 |  |
| DISPLAY average | 10 | 20 | 15 | 15 |

The table makes the repair visible.

## 7. Finding wrong order with a trace

Broken design:

```text
BEGIN
  SET total = price + tax
  INPUT price
  SET tax = price * 0.1
  DISPLAY total
END
```

Sample intended price: 50. Expected tax: 5. Expected total: 55.

Attempted trace:

| Step | price | tax | total | Output | Problem |
| --- | --- | --- | --- | --- | --- |
| SET total = price + tax | ? | ? | ? |  | uses unset names |
| INPUT price | 50 | ? | ? |  | total already wrongly set |
| SET tax = price * 0.1 | 50 | 5 | ? |  | total not updated |
| DISPLAY total | 50 | 5 | ? | ? | total never corrected |

Even before finishing numbers, the table shows order failure: `total` is computed too early and never recomputed after `tax` exists.

Correct order:

```text
BEGIN
  INPUT price
  SET tax = price * 0.1
  SET total = price + tax
  DISPLAY total
END
```

| Step | price | tax | total | Output |
| --- | --- | --- | --- | --- |
| INPUT price | 50 |  |  |  |
| SET tax = price * 0.1 | 50 | 5 |  |  |
| SET total = price + tax | 50 | 5 | 55 |  |
| DISPLAY total | 50 | 5 | 55 | 55 |

Wrong order and wrong formulas both appear clearly when you force every step onto paper.

## 8. Choose sample values that reveal mistakes

Not every sample exposes every bug. Choose values with intention.

### Use easy values first

Easy values check basic flow.

- prices like 10, 20, 50
- quantities like 1, 2, 3
- scores like 80, 90, 100

If the design fails on easy values, fix that before fancy cases.

### Use values with known expected results

Pick numbers you can compute mentally or with simple arithmetic.

Example: average of 70, 80, 90 should be 80. If the table shows 185, you know the formula is wrong.

### Use values that exercise rates and parentheses

Discount and tax designs need samples where the decimal rate matters.

- price 100 with 10 percent discount expects discount amount 10
- price 50 with 8 percent tax expects tax 4

If someone multiplies by `10` instead of `0.10`, the trace explodes to an obviously wrong total.

### Use more than one sample when needed

A design might pass one lucky sample and fail another.

Example broken average divisor:

```text
SET average = (score1 + score2 + score3) / 2
```

Lucky? Not really for three equal scores, but different samples help. With 10, 10, 10:

- wrong design average: 15
- correct average: 10

The mismatch is obvious.

### Include zero when it is valid

For totals, quantity `0` may be valid and should produce total `0`. For averages, dividing by a count of zero is a different problem (later selection or validation modules). At this stage, choose counts that make sense for the stated problem.

## 9. Trace tables and flowcharts together

You can desk-check from pseudocode or from a flowchart. The method is the same:

1. Start at `BEGIN` / `START`.
2. Move to the next instruction or symbol.
3. Update the table.
4. Stop at `END`.

If the flowchart and pseudocode disagree, the trace will follow whichever document you are reading. That is another reason to keep both designs matched (Module 05).

## 10. Worked example: discount then tax

Design:

```text
BEGIN
  CONSTANT DISCOUNT_RATE = 0.20
  CONSTANT TAX_RATE = 0.05
  INPUT originalPrice
  SET discountAmount = originalPrice * DISCOUNT_RATE
  SET discountedPrice = originalPrice - discountAmount
  SET tax = discountedPrice * TAX_RATE
  SET amountDue = discountedPrice + tax
  DISPLAY amountDue
END
```

Sample: `originalPrice = 200`.

Expected:

- discount amount 40
- discounted price 160
- tax 8
- amount due 168

Trace table:

| Step | originalPrice | discountAmount | discountedPrice | tax | amountDue | Output |
| --- | --- | --- | --- | --- | --- | --- |
| INPUT originalPrice | 200 |  |  |  |  |  |
| SET discountAmount | 200 | 40 |  |  |  |  |
| SET discountedPrice | 200 | 40 | 160 |  |  |  |
| SET tax | 200 | 40 | 160 | 8 |  |  |
| SET amountDue | 200 | 40 | 160 | 8 | 168 |  |
| DISPLAY amountDue | 200 | 40 | 160 | 8 | 168 | 168 |

Because each intermediate value is visible, you can locate an error in seconds. If `tax` were 10 instead of 8, you would inspect the tax line and the rate, not rewrite the whole design at random.

## 11. How to write a clean desk-check routine

Use this routine for every non-trivial sequential design:

1. Restate the expected result for one sample in plain words and numbers.
2. List variable columns.
3. Fill the table instruction by instruction.
4. Compare final output (and key middle values) with the expected result.
5. If they differ, find the first row that goes wrong.
6. Fix the design at that point.
7. Re-trace with the same sample.
8. Trace a second sample when rates, counts, or order could still hide a bug.

The first wrong row is the key. Do not only stare at the final answer. Intermediate values show where logic drifted.

## 12. What a trace table can and cannot prove

A successful trace for one sample shows the design works for that sample. It does not prove the design works for every possible input.

Still, desk checking is powerful for beginner sequential logic because many bugs appear immediately:

- wrong operator order
- missing parentheses
- reversed steps
- wrong divisor
- rate written as 15 instead of 0.15
- displayed the wrong variable

Later topics (selection, loops, arrays) make tracing even more important. Learning the table habit now prepares you for those modules.

## Common mistakes

1. **Skipping steps in the table**  
   Jumping from inputs straight to the final answer hides the first wrong assignment.

2. **Changing several variables in one unclear row**  
   Prefer one main instruction per row while learning.

3. **Using sample values that are hard to compute by hand**  
   Choose numbers that make expected results obvious.

4. **Forgetting the Output column**  
   Then you cannot quickly compare displayed results with the requirement.

5. **Not fixing and re-tracing after a failure**  
   A repair is not confirmed until a new table matches the expected result.

6. **Assuming the design is perfect because the flowchart is neat**  
   Layout quality and logic quality are different. Trace the logic.

7. **Stopping after one lucky sample**  
   When formulas involve rates or counts, use a second sample.

## Check your understanding

1. What is a trace table?
2. Why should you evaluate one instruction per row while learning?
3. A design should average 8 and 12. A trace shows output 14. What kind of formula mistake might cause that?
4. Why are easy sample values with known expected results useful?
5. Does one successful trace prove a design is correct for all inputs? Why or why not?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

Module 09 introduces modules and hierarchy charts. You will split larger solutions into smaller named parts and show how those parts relate.
