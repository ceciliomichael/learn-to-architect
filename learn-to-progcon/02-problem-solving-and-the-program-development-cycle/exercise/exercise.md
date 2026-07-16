# Module 02 Exercises

Complete these tasks with paper or a text editor. No programming language is required.

## Warm-up: Rewrite a weak problem statement

This statement is too vague:

```text
Handle store prices.
```

1. Rewrite it as a clear problem statement for one specific task (for example, a total with tax, or a discount price).
2. List the inputs.
3. List the output.
4. Write one sentence that states the main rule or formula.

## Guided exercise: Walk the full cycle

Problem:

```text
A student has two exam scores. Calculate and show the average of the two scores.
```

Follow these steps in order:

1. **Understand**: write a one-sentence problem statement in your own words. Note one unusual case you might care about later (for example, scores outside 0 to 100).
2. **Plan**: write numbered logic steps.
3. **Write**: copy the plan into a clean final design with clear names (score1, score2, average).
4. **Test**: choose two sample pairs of scores. For each pair, show the hand-check math and the expected average.
5. **Maintain and document**: write three short documentation lines: problem, formula, and one sample test with expected result.

## Independent exercise: IPO and rework

A cafe wants this:

```text
Read the drink price and a tip percent. Show the tip amount and the total payment (price plus tip).
```

Requirements:

1. Build an IPO chart with three parts: Input, Process, Output.
2. Write a numbered plan that matches the IPO chart.
3. Desk-check with price `12.00` and tip percent `15` (meaning 15%). Show the expected tip amount and total.
4. Describe one rework problem that would happen if someone skipped the understand step and assumed tip percent was already a decimal such as `0.15` while the cashier always types `15`.
5. Describe one rework problem that would happen if someone skipped testing.

## Debugging / desk-check task

A learner claims this "cycle" is complete for a tax total program. Find what is missing or wrong. Then rewrite a correct mini cycle for the same problem.

Learner notes:

```text
Understand: do tax
Plan: (none, I already know how stores work)
Write: show price * 1.08
Test: it looked right on one try with some number I forgot
Maintain: not needed because the program is finished forever
```

Your rewrite must include all five cycle steps with enough detail that another student could follow them for price input and 8% tax.

## Completion checklist

- [ ] I rewrote a vague problem into a clear statement with inputs and output.
- [ ] I applied understand, plan, write, test, and document to the two-score average.
- [ ] I built an IPO chart and desk-checked a tip calculation.
- [ ] I explained rework from skipping understand and skipping test.
- [ ] I repaired the incomplete tax-total cycle notes.

When you have made a real attempt, compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md).
