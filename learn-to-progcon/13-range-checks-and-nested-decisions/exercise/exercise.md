# Module 13 Exercises

## Warm-up: Comfort temperature

A room is comfortable when the temperature is between 18 and 24 inclusive.

1. Write a range condition for `temperature`.
2. Predict true or false for these values: 17, 18, 21, 24, 25.
3. Write a short IF that displays "Comfortable" or "Adjust climate".

## Guided exercise: Letter grades

Write a multi-way selection that assigns a letter grade from a test score.

Rules:

- 90 to 100: A
- 80 to 89: B
- 70 to 79: C
- 60 to 69: D
- 0 to 59: F
- any other score: Invalid

Steps:

1. Write the plain English rules in order from A down to Invalid.
2. Write the pseudocode with ELSE IF.
3. Build a trace table for scores 95, 80, 72, 60, 40, and 105.
4. Confirm each score lands in exactly one band.

## Independent exercise: Bus ticket price

Design a module that sets a ticket price from age.

Rules:

- age under 0: display "Invalid age" and stop
- age 0 through 4: free (price 0)
- age 5 through 17: child price 1.50
- age 18 through 64: adult price 2.75
- age 65 and older: senior price 1.25

Requirements:

- Use multi-way selection.
- Input age.
- Display either the error message or the price.
- Include a small flowchart in text form for the decision structure.
- Desk-check ages -1, 3, 12, 30, and 70.

## Debugging / desk-check task

This design is wrong for score 92. It should print "Excellent".

```text
Set score = 92

IF score >= 60 THEN
    Display "Pass"
ELSE IF score >= 90 THEN
    Display "Excellent"
ELSE
    Display "Needs work"
END IF
```

1. Trace the design with score 92. Which branch runs?
2. Explain why "Excellent" never runs.
3. Rewrite the design so 92 prints "Excellent", 75 prints "Pass", and 50 prints "Needs work".
4. Optional second fix: rewrite with full range checks for 90-100, 60-89, and below 60, plus an out-of-range message for scores outside 0 to 100.

## Completion checklist

- [ ] I wrote a correct inclusive range with AND.
- [ ] I built a multi-way grade design and traced several scores.
- [ ] I designed ticket prices with clear age bands.
- [ ] I fixed a condition-order bug and explained the mistake.
- [ ] I checked boundary values, not only middle values.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
