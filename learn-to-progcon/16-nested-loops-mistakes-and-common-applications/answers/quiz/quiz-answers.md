# Module 16 Quiz Answers

## Answer 1

The inner body runs 3 * 4 = 12 times.

Each of the 3 outer passes fully completes the inner loop of 4 repetitions.

## Answer 2

A counter tracks how many times an event happened, usually by adding 1.

```text
Set count = count + 1
```

An accumulator builds a running total by adding a varying amount.

```text
Set total = total + amount
```

## Answer 3

The design reads a new score before adding, so the first valid score is skipped. Depending on timing, the sentinel -1 can also be added.

Correct pattern: process the current score, then read the next one.

```text
Set total = 0
Input score
WHILE score <> -1
    Set total = total + score
    Input score
END WHILE
```

## Answer 4

Any two valid pairs are fine. Strong answers include:

1. **Reusing the same control variable in outer and inner loops.**  
   Prevent it by naming separate variables such as `row` and `col`.

2. **Forgetting to reset an inner accumulator on each outer pass.**  
   Prevent it by setting the team or group total to 0 at the start of each outer iteration, and desk-checking two groups.

3. **Off-by-one on start or stop.**  
   Prevent it by stating first value, last value, and expected count, then tracing both ends.

4. **Missing update in a WHILE condition.**  
   Prevent it by naming the control variable and finding its update line before finishing the design.

## Answer 5

This problem mixes indefinite stopping with a counted limit.

- It is indefinite in spirit because success may happen on attempt 1, 2, or 3.
- A counter tracks how many attempts were used.
- A maximum of 3 attempts makes the loop stop even when the PIN stays wrong.
- Nested loops are not required.
- A sentinel is not the main idea here, unless you invent one. The stop rules are "PIN correct" or "tries used up."

Sample design:

```text
Set tries = 1
Input pin
WHILE pin <> "1234" AND tries < 3
    Display "Incorrect PIN"
    Set tries = tries + 1
    Input pin
END WHILE

IF pin = "1234" THEN
    Display "Access granted"
ELSE
    Display "Access denied"
END IF
```
