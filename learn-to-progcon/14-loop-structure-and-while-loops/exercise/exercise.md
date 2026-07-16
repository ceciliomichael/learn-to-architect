# Module 14 Exercises

## Warm-up: Count from 1 to 4

Write a WHILE loop that displays 1, 2, 3, and 4 on separate lines, then displays "Finished".

1. Initialize a counter.
2. Write the WHILE condition.
3. Display the counter and update it in the body.
4. Trace every check until the loop exits.

## Guided exercise: Sum until zero

Design a module that reads numbers until the user enters 0, then displays the sum of the numbers entered before 0.

Steps:

1. Initialize `total` to 0.
2. Use a priming input for `number`.
3. WHILE `number` is not 0, add it to `total` and read the next number.
4. After the loop, display `total`.
5. Desk-check the inputs 4, 6, 5, 0. Expected total is 15.
6. Confirm that 0 is not added to the total.

## Independent exercise: Attendance counter

A club reads names until the user enters the word STOP. Count how many names were entered before STOP and display the count.

Requirements:

- Use a WHILE loop with a priming read.
- Do not count STOP as a name.
- Display a clear final message such as the count alone or "Members: " followed by the count.
- Include a text flowchart for the loop.
- Desk-check the name list Ana, Ben, Cam, STOP. Expected count is 3.

## Debugging / desk-check task

This design is supposed to display 5, 4, 3, 2, 1 and then "Lift off". It is broken.

```text
Set n = 5

WHILE n > 0
    Display n
END WHILE

Display "Lift off"
```

1. Explain why the loop is infinite.
2. Rewrite the design so it counts down correctly.
3. Build a short trace table for your fixed version.
4. Second bug to fix: this version updates the wrong way for a countdown.

```text
Set n = 5

WHILE n > 0
    Display n
    Set n = n + 1
END WHILE
```

Explain what happens and correct the update.

## Completion checklist

- [ ] I wrote a counted WHILE loop and traced it.
- [ ] I used a priming read for a sentinel-controlled sum.
- [ ] I designed an attendance loop that does not count the stop value.
- [ ] I diagnosed and fixed infinite-loop mistakes.
- [ ] I can name the control variable, its test, and its update in each design.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
