# Module 15: For Loops, Definite Loops, and Indefinite Loops

## Before you start

Complete Modules 01 to 14. You should already know:

- WHILE loops and loop control variables
- priming reads for input-controlled loops
- how to avoid infinite loops
- selection, ranges, modules, and trace tables

You will keep designing in pseudocode and flowcharts.

## What you will learn

- tell definite loops from indefinite loops
- design a FOR loop for counted repetition
- set counter start, stop, and step values correctly
- choose WHILE when the end depends on a condition, and FOR when the count is known
- rewrite simple counted WHILE loops as FOR loops

## Why this matters

Some jobs have a known number of repeats: print 10 labels, read 5 scores, or run 3 attempts. Other jobs stop only when something happens: the user types DONE, a password is accepted, or a total passes a limit. Matching the loop form to the problem makes designs shorter and safer.

## 1. Definite loops and indefinite loops

A **definite loop** repeats a known number of times. You can state the count before the loop starts, or compute it from a value you already have.

Examples of definite loops:

- display the numbers 1 through 10
- read marks for exactly 30 students
- add the prices of 4 items

An **indefinite loop** repeats an unknown number of times. You know how to stop, but not how many passes will happen.

Examples of indefinite loops:

- read scores until the user enters -1
- keep asking for a password until it is correct
- add expenses until the budget is used up

| question | definite | indefinite |
| --- | --- | --- |
| Do I know the count up front? | yes | no |
| Typical control | counter with start and stop | condition, often with new input or a flag |
| Common structure | FOR, or WHILE with a counter | WHILE |

"Indefinite" does not mean "never ends." It means the count is not fixed in advance. A correct indefinite loop still has a clear stop rule.

## 2. FOR loop structure for counted work

A **FOR loop** is a counted loop. In design form, it states the counter, where it starts, where it stops, and how it changes.

Common pseudocode form:

```text
FOR counter = start TO stop STEP stepValue
    statement
    statement
END FOR
```

If the step is 1, many designs omit STEP:

```text
FOR count = 1 TO 5
    Display count
END FOR
```

Meaning:

1. Set `count` to 1.
2. If `count` is past 5, leave the loop.
3. Run the body.
4. Add the step (here, 1) to `count`.
5. Go back to the test.

Output:

```text
1
2
3
4
5
```

### FOR parts named clearly

| part | meaning | example |
| --- | --- | --- |
| counter | loop control variable | `count` |
| start | first value of the counter | 1 |
| stop | final value that still runs | 5 |
| step | amount added each time | 1 |

Some languages use different keywords. The design idea stays the same: start, test against stop, body, then step.

## 3. Start, stop, and step

### Counting upward

```text
FOR n = 1 TO 4 STEP 1
    Display n
END FOR
```

Values of `n`: 1, 2, 3, 4.

### Counting by a larger step

```text
FOR n = 0 TO 10 STEP 2
    Display n
END FOR
```

Values of `n`: 0, 2, 4, 6, 8, 10.

### Counting downward

```text
FOR n = 5 TO 1 STEP -1
    Display n
END FOR
```

Values of `n`: 5, 4, 3, 2, 1.

When the step is negative, the counter moves down. The loop continues while the counter has not passed the stop value in that direction.

### Off-by-one thinking

Ask:

- What is the first value that should run?
- What is the last value that should run?
- Does the stop value itself run? In `FOR n = 1 TO 5`, yes, 5 runs.

If you need 5 repetitions starting at 1, stop at 5 with step 1. If you need the values 0 through 4, that is also 5 repetitions, but the start and stop differ.

## 4. Predict the result

```text
Set total = 0

FOR k = 1 TO 4
    Set total = total + k
END FOR

Display total
```

Trace:

| k | total after adding k |
| --- | --- |
| 1 | 1 |
| 2 | 3 |
| 3 | 6 |
| 4 | 10 |

Displayed result:

```text
10
```

## 5. FOR flowchart idea

A FOR loop still has initialize, test, body, and update. The FOR heading packages those pieces.

```text
                 [Start]
                    |
          counter = start
                    |
                    v
         +----------------------+
    +--->| counter past stop?   |
    |    +----------+-----------+
    |          no /               \ yes
    |            /                 \
    |      [loop body]          after loop
    |            |
    |   counter = counter + step
    |            |
    +------------+
```

"Past stop" depends on direction. With a positive step, leave when counter is greater than stop. With a negative step, leave when counter is less than stop.

## 6. Rewrite a counted WHILE as a FOR

WHILE form:

```text
Set count = 1
WHILE count <= 3
    Display count
    Set count = count + 1
END WHILE
```

FOR form:

```text
FOR count = 1 TO 3
    Display count
END FOR
```

Both display:

```text
1
2
3
```

Use FOR when the main idea is "repeat from here to there." Use WHILE when the main idea is "repeat while this condition holds," especially with input or flags.

## 7. When to choose WHILE vs FOR

Choose **FOR** when:

- you know how many times to repeat
- a counter is the natural control
- start, stop, and step are clear

Choose **WHILE** when:

- the number of repeats is unknown
- a sentinel value ends the loop
- validation must repeat until input is legal
- a flag or changing condition is clearer than a fixed count

### Side-by-side example: five scores

FOR is a natural fit:

```text
Set total = 0

FOR i = 1 TO 5
    Input score
    Set total = total + score
END FOR

Set average = total / 5
Display average
```

### Side-by-side example: scores until -1

WHILE is the natural fit:

```text
Set total = 0
Set count = 0

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
    Display "No scores entered"
END IF
```

You could force either problem into the other loop form, but the design becomes harder to read.

## 8. Definite loop from a stored count

The count does not have to be a literal number. It can be a variable.

```text
Input studentCount
Set total = 0

FOR i = 1 TO studentCount
    Input mark
    Set total = total + mark
END FOR

IF studentCount > 0 THEN
    Set average = total / studentCount
    Display average
ELSE
    Display "No students"
END IF
```

Once `studentCount` is known, the loop is definite even though different classes have different sizes.

## 9. Worked example: price list with a step

Problem: display sample prices from 10 to 50 increasing by 10.

```text
Module PriceSamples
    FOR price = 10 TO 50 STEP 10
        Display price
    END FOR
End Module
```

Output:

```text
10
20
30
40
50
```

## 10. Worked example: attendance for a known class size

Problem: for each of 4 students, input present as true or false, and count how many are present.

```text
Module ClassAttendance
    Set presentCount = 0

    FOR student = 1 TO 4
        Input isPresent
        IF isPresent = true THEN
            Set presentCount = presentCount + 1
        END IF
    END FOR

    Display presentCount
End Module
```

Trace with true, false, true, true:

| student | isPresent | presentCount after IF |
| --- | --- | --- |
| 1 | true | 1 |
| 2 | false | 1 |
| 3 | true | 2 |
| 4 | true | 3 |

Displayed count: 3.

## 11. Indefinite loop reminder: sentinel control

A **sentinel** is a special value that means "stop," not "process this as normal data."

```text
Set total = 0

Input amount
WHILE amount <> 0
    Set total = total + amount
    Input amount
END WHILE

Display total
```

This is indefinite because the user decides when to stop. FOR would be the wrong first choice unless you already know how many amounts will arrive.

## 12. Choosing under pressure: a quick test

Ask these questions in order:

1. Do I know the number of repetitions before the loop starts?
2. If yes, can I write start, stop, and step cleanly? Prefer FOR.
3. If no, what condition means "keep going"? Prefer WHILE.
4. If input controls stopping, do I need a priming read?

If you cannot answer question 3 for a WHILE, the loop is not ready.

## Common mistakes

1. **Using FOR for a sentinel loop.**  
   Sentinel input is usually a WHILE problem.

2. **Wrong stop value.**  
   `FOR i = 1 TO 4` runs four times. People sometimes expect three or five. Trace the ends.

3. **Forgetting that the stop value is included in the basic TO form.**  
   1 TO 5 includes 5 when the step is 1.

4. **Using the wrong step sign.**  
   Counting down needs a negative step. A positive step from 5 to 1 never moves toward 1.

5. **Changing the FOR counter in confusing ways inside the body.**  
   Extra changes to the counter make the loop hard to predict. Prefer a clear step in the heading.

6. **Dividing by a count that can be zero.**  
   After an indefinite loop, check that at least one real value was processed before computing an average.

## Check your understanding

1. Is "read names until STOP" definite or indefinite? Which loop form fits best?
2. What values does `FOR n = 3 TO 9 STEP 3` produce?
3. Rewrite this as a FOR loop:

```text
Set i = 1
WHILE i <= 4
    Display i
    Set i = i + 1
END WHILE
```

4. When is a WHILE still better even if you could invent a huge maximum count?
5. Why is `studentCount` allowed as the stop value in a FOR loop?

## Practice

Complete the practice tasks in [exercise/exercise.md](./exercise/exercise.md).

Then take the quiz in [quiz/quiz.md](./quiz/quiz.md).

## Next step

Module 16 covers nested loops, common loop mistakes, counters, accumulators, sentinels, and everyday applications such as totals, retries, and simple tables.
