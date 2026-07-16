# Module 16: Nested Loops, Mistakes, and Common Applications

## Before you start

Complete Modules 01 to 15. You should already know:

- WHILE and FOR loop structure
- definite and indefinite loops
- priming reads and sentinels
- counters, simple running totals, selection, and trace tables

This module stays in pseudocode and flowchart thinking.

## What you will learn

- write nested loops where one loop sits inside another
- avoid common loop mistakes such as off-by-one errors and forgotten updates
- use counters and accumulators on purpose
- design sentinel-controlled input carefully
- apply loops to totals, validation retries, and simple tables or grids

## Why this matters

Many real tasks are loops of loops. A teacher has classes, and each class has students. A shop has days, and each day has sales. A seating chart has rows and seats. Nested loops describe those patterns. Counters, accumulators, and sentinels turn the same loop tools into practical designs.

## 1. Nested loops: a loop inside a loop

A **nested loop** places one loop inside the body of another loop.

- The **outer loop** controls the bigger cycle.
- The **inner loop** runs completely for each single pass of the outer loop.

Example: for each of 3 rows, display 4 seat numbers.

```text
FOR row = 1 TO 3
    FOR seat = 1 TO 4
        Display row
        Display seat
    END FOR
END FOR
```

How many times does the inner body run?

3 rows times 4 seats = 12 times.

### Trace the pattern

| outer row | inner seat values |
| --- | --- |
| 1 | 1, 2, 3, 4 |
| 2 | 1, 2, 3, 4 |
| 3 | 1, 2, 3, 4 |

The inner counter restarts for every new outer value. That restart is normal and required.

### Nested loop flowchart sketch

```text
                 [Start]
                    |
              row = 1
                    |
                    v
         +--------------------+
    +--->| row past 3?        |
    |    +---------+----------+
    |         no /              \ yes
    |           /                \
    |     seat = 1             [End]
    |           |
    |           v
    |  +------------------+
    |  | seat past 4?     |<------+
    |  +--------+---------+       |
    |      no /           \ yes   |
    |        /             \      |
    |  display row,seat   row = row + 1
    |        |               |
    |  seat = seat + 1       |
    |        |               |
    |        +---------------+
    |                        |
    +------------------------+
```

## 2. Use different control variables

Each loop level needs its own control variable.

Clear:

```text
FOR row = 1 TO 3
    FOR col = 1 TO 5
        Display row
        Display col
    END FOR
END FOR
```

Confusing and wrong:

```text
FOR i = 1 TO 3
    FOR i = 1 TO 5
        Display i
    END FOR
END FOR
```

Reusing the same counter for outer and inner loops overwrites the outer control. The nested structure then fails in hard-to-trace ways. Name variables by role: `row` and `seat`, `day` and `sale`, `student` and `attempt`.

## 3. Common loop mistakes

### Mistake A: Off-by-one

An **off-by-one error** runs one time too many or one time too few.

Intended: display 1 through 5.

Too few:

```text
FOR n = 1 TO 4
    Display n
END FOR
```

Too many if you meant 1 through 4:

```text
FOR n = 1 TO 5
    Display n
END FOR
```

Fix method: state the first value, the last value, and the count. Then choose start and stop to match. Desk-check the first and last passes.

### Mistake B: Forgetting to update the control variable

```text
Set count = 1
WHILE count <= 3
    Display count
END WHILE
```

This never ends. Add `Set count = count + 1` in the body.

### Mistake C: Wrong condition

```text
Set total = 0
Input value
WHILE value = -1
    Set total = total + value
    Input value
END WHILE
```

This loop runs only when the value is already -1. The condition should be `value <> -1` for a normal sentinel sum.

### Mistake D: Same control variable used incorrectly in nests

Covered above. Give each loop its own counter.

### Mistake E: Updating the counter in both the FOR heading and the body

```text
FOR i = 1 TO 5
    Display i
    Set i = i + 1
END FOR
```

The extra body update can skip values. Prefer one clear step in the FOR heading.

### Mistake F: Using the sentinel as real data

```text
Input score
WHILE score <> -1
    Input score
    Set total = total + score
END WHILE
```

Here the first score is never added, and a final -1 might be added depending on order. Use process-then-read or the standard priming pattern carefully so only real data is accumulated.

## 4. Counters and accumulators

A **counter** counts how many times something happened. It usually increases by 1.

```text
Set count = count + 1
```

An **accumulator** builds a running total. It increases by a varying amount.

```text
Set total = total + amount
```

Both must be initialized before the loop:

```text
Set count = 0
Set total = 0
```

### Together in one loop

```text
Set count = 0
Set total = 0

Input score
WHILE score <> -1
    Set total = total + score
    Set count = count + 1
    Input score
END WHILE

IF count > 0 THEN
    Set average = total / count
    Display average
ELSE
    Display "No scores"
END IF
```

Roles:

- `score` controls when the loop stops
- `total` accumulates score values
- `count` counts how many scores were added

## 5. Sentinel-controlled input

A **sentinel** is a special end marker. It is not ordinary data.

Good sentinel habits:

1. Tell the user what value ends input.
2. Choose a sentinel that cannot be valid data, or handle the rule carefully.
3. Use a priming read.
4. Test for the sentinel before processing.
5. Read the next value at the end of the body.

Example: shopping prices end with 0.

```text
Module CartTotal
    Set total = 0
    Set itemCount = 0

    Display "Enter price, or 0 to finish"
    Input price

    WHILE price <> 0
        IF price > 0 THEN
            Set total = total + price
            Set itemCount = itemCount + 1
        ELSE
            Display "Price must be positive"
        END IF
        Input price
    END WHILE

    Display itemCount
    Display total
End Module
```

Zero ends the loop. Negative prices can be rejected without ending the session if your rule says so.

## 6. Application: totals and averages

```text
Module WeeklyTotal
    Set total = 0

    FOR day = 1 TO 7
        Input sales
        Set total = total + sales
    END FOR

    Display total
    Set average = total / 7
    Display average
End Module
```

This is definite: seven days. The accumulator `total` holds the week sum.

## 7. Application: validation retries

Keep asking until the input is legal, or until a maximum number of tries is used.

### Until valid, no try limit

```text
Input age
WHILE age < 0 OR age > 120
    Display "Enter age from 0 to 120"
    Input age
END WHILE
```

### Limited retries

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

Trace with wrong, wrong, correct:

| tries before body end | pin entered | notes |
| --- | --- | --- |
| priming | wrong1 | fails, tries becomes 2 |
| 2 | wrong2 | fails, tries becomes 3 |
| 3 | 1234 | condition false because pin matches, leave loop |

Access granted.

## 8. Application: simple tables and grids

Nested loops are useful for rectangular layouts.

### Multiplication table cells for 1 through 3

```text
FOR row = 1 TO 3
    FOR col = 1 TO 3
        Set product = row * col
        Display product
    END FOR
END FOR
```

Values in order:

```text
1 2 3
2 4 6
3 6 9
```

(Each product may appear on its own line in a simple display design.)

### Classroom grid: 2 groups, 3 scores each

```text
FOR group = 1 TO 2
    Set groupTotal = 0
    FOR member = 1 TO 3
        Input score
        Set groupTotal = groupTotal + score
    END FOR
    Display group
    Display groupTotal
END FOR
```

The inner loop finishes one group. The outer loop moves to the next group. Notice `groupTotal` is reset for each outer pass.

## 9. Predict the result

```text
Set stars = ""
FOR line = 1 TO 3
    FOR count = 1 TO line
        Set stars = stars + "*"
    END FOR
    Display stars
    Set stars = ""
END FOR
```

If your design language builds text this way, the displays are:

```text
*
**
***
```

Line 1 prints one star. Line 2 prints two stars. Line 3 prints three stars. The outer loop chooses the line. The inner loop chooses how many stars that line needs.

A pure numeric version without string building:

```text
FOR line = 1 TO 3
    FOR count = 1 TO line
        Display "*"
    END FOR
END FOR
```

That version prints each star separately. The nested structure is the same idea.

## 10. Worked example: nested class processing

Problem: a school has 2 classes. Each class has 3 students. Read a mark for every student. Display each class average, then the school total of all marks.

```text
Module TwoClassMarks
    Set schoolTotal = 0

    FOR classNumber = 1 TO 2
        Set classTotal = 0

        FOR student = 1 TO 3
            Input mark
            Set classTotal = classTotal + mark
            Set schoolTotal = schoolTotal + mark
        END FOR

        Set classAverage = classTotal / 3
        Display classNumber
        Display classAverage
    END FOR

    Display schoolTotal
End Module
```

Sample marks:

- Class 1: 70, 80, 90
- Class 2: 60, 65, 75

| class | classTotal | classAverage | schoolTotal after class |
| --- | --- | --- | --- |
| 1 | 240 | 80 | 240 |
| 2 | 200 | about 66.67 | 440 |

Displays: class 1 average 80, class 2 average 200/3, school total 440.

## 11. Desk-check strategy for nested loops

When nested loops misbehave, do not guess. Build a table with:

1. outer control value
2. inner control value
3. any accumulator or counter
4. output or important assignment

Check:

- Does the inner loop restart for every outer pass?
- Is each total reset at the right time?
- Are start and stop values inclusive as intended?
- Does every WHILE have an update?

## Common mistakes

1. **Off-by-one on start or stop.**  
   Trace the first and last values every time.

2. **Forgotten update in WHILE.**  
   Infinite loop.

3. **Wrong condition, especially `=` instead of `<>` with sentinels.**  
   The loop may never enter or never leave as you expect.

4. **Reusing one counter for two nested loops.**  
   Outer progress is destroyed.

5. **Failing to reset an accumulator between outer passes.**  
   Group 2 totals then include Group 1 by accident.

6. **Counting the sentinel or adding it into a total.**  
   Keep the stop value out of processing.

7. **Dividing by zero after an empty indefinite loop.**  
   Check `count > 0` before an average.

## Check your understanding

1. If the outer loop runs 4 times and the inner loop runs 5 times per outer pass, how many times does the inner body run?
2. What is the difference between a counter and an accumulator?
3. Why must nested loops use different control variables?
4. Write the standard priming-read pattern for summing numbers until -1.
5. Name three common loop mistakes and one way to catch each with a desk check.

## Practice

Complete the practice tasks in [exercise/exercise.md](./exercise/exercise.md).

Then take the quiz in [quiz/quiz.md](./quiz/quiz.md).

## Next step

Module 17 introduces arrays: named lists of related values stored in order, with indexes for reading and writing individual elements.
