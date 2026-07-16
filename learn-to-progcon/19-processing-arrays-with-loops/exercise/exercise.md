# Module 19 Exercises

Use pseudocode and trace tables. No Python required.

## Warm-up: Change a working total

Start with:

```text
SET prices = [10, 4, 7]
SET total = 0
FOR index FROM 0 TO 2 STEP 1
    SET total = total + prices[index]
END FOR
OUTPUT total
```

1. Add a fourth price `9` and fix the loop bounds.
2. Also compute and output the average.
3. Desk-check the final total and average.

## Guided exercise: Class scores report

Scores:

```text
88, 76, 95, 81, 90
```

Design a program that:

1. Stores the scores in an array.
2. Prints every score.
3. Prints the total.
4. Prints the average.
5. Prints the highest score.
6. Prints the lowest score.

Include a short trace for the highest-score loop.

## Independent exercise: Partial temperature log

An array can hold up to 7 temperatures. Only the first 4 slots are filled:

```text
18, 21, 19, 22
```

Logical size `count = 4`.

Requirements:

- Store values in an array with capacity 7 (unused slots may be 0).
- Use `count` in all processing loops.
- Output all valid temperatures.
- Output the average of the valid temperatures only.
- Explain why looping to index 6 would be wrong for the average.

## Debugging / desk-check task

Find and fix the bugs:

```text
SET nums = [5, 2, 9]
SET total = 0
SET maximum = 0
FOR index FROM 0 TO 3 STEP 1
    SET total = total + nums[index]
    IF nums[index] > maximum THEN
        SET maximum = nums[index]
    END IF
END FOR
SET average = total / 3
OUTPUT total
OUTPUT average
OUTPUT maximum
```

Write the corrected design and expected outputs.

## Completion checklist

- [ ] I computed sum and average with a loop.
- [ ] I found min and max starting from the first element.
- [ ] I used logical size correctly for a partial fill.
- [ ] I desk-checked at least one accumulator loop.
- [ ] I fixed off-by-one and bad max-start mistakes.

When you have made a real attempt, compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md).
