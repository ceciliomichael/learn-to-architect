# Module 08 Quiz Answers

## Answer 1

Desk checking means following a design by hand, as if you were the computer. You update stored values and note outputs for sample data.

A trace table supports desk checking by recording those values in columns and rows. The written history makes wrong formulas, wrong order, and wrong outputs easier to see and explain.

## Answer 2

| Step | x | y | sum | Output |
| --- | --- | --- | --- | --- |
| INPUT x | 9 |  |  |  |
| INPUT y | 9 | 1 |  |  |
| SET sum = x + y | 9 | 1 | 10 |  |
| DISPLAY sum | 9 | 1 | 10 | 10 |

## Answer 3

Correct discounted value for price 40:

- `discounted = 40 - (40 * 0.5)`
- `discounted = 40 - 20`
- `discounted = 20`

If a learner uses `SET discounted = price - 0.5`:

- `discounted = 40 - 0.5 = 39.5`

That sample is useful because the wrong result is clearly not a 50 percent discount. A price of 40 with half off must land at 20, not 39.5.

## Answer 4

The final output only shows that something ended wrong or right. The first wrong row shows the exact instruction where memory diverged from the intended plan. That is the best place to repair the design.

## Answer 5

No. One successful sample shows the design works for that sample. Other inputs might still expose a wrong divisor, bad rate, or order problem. Desk checking reduces risk. It does not mathematically prove correctness for every possible input.
