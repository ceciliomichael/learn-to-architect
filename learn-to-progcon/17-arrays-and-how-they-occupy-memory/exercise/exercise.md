# Module 17 Exercises

Complete these tasks in pseudocode or clear design notes. You do not need Python yet.

## Warm-up: Change a working design

Start with:

```text
SET colors = ["red", "green", "blue"]
OUTPUT colors[0]
OUTPUT colors[1]
OUTPUT colors[2]
```

1. Change the middle color to `"yellow"`.
2. Add a fourth color `"purple"` so the array has size 4.
3. Output all four colors with a FOR loop from index 0 to 3.

## Guided exercise: Five quiz scores

Design a program that:

1. Stores five quiz scores in an array named `scores`.
2. Uses sample values `80, 90, 70, 85, 95` for now.
3. Outputs each score on its own line using a loop.
4. Outputs the first score and the last score again with clear labels.

Follow these steps:

1. Write the array setup.
2. Write the loop that prints every element.
3. Write two OUTPUT lines for first and last using indexes `0` and `4`.
4. Desk-check one loop pass for index `2` and confirm the value is `70`.

## Independent exercise: Daily temperatures

A weather log stores seven daily high temperatures in Celsius:

```text
22, 24, 21, 19, 25, 27, 23
```

Requirements:

- Store them in an array named `highs`.
- Output the temperature for day index `0` and day index `6` with labels.
- Change day index `3` to `20` (a corrected reading).
- Output the full updated list with a loop.
- State the array size and the valid index range in a short comment or note.

## Debugging / desk-check task

This design is wrong. Find and fix the problems.

```text
SET prices = [10, 4, 7]
SET total = 0
FOR index FROM 0 TO 3 STEP 1
    SET total = total + prices[index]
END FOR
OUTPUT total
OUTPUT "First price is" prices[1]
```

Issues to consider:

- loop stop index
- which index is first
- whether every access is valid

Write the corrected design and the correct total.

## Completion checklist

- [ ] I can declare or set an array with several related values.
- [ ] I can name size and valid 0-based indexes.
- [ ] I can read and write `array[index]`.
- [ ] I can loop through every element.
- [ ] I fixed an off-by-one index mistake.

When you have made a real attempt, compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md).
