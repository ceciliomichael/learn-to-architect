# Module 14: Loop Structure and While Loops

## Before you start

Complete Modules 01 to 13. You should already know:

- variables, assignment, and arithmetic
- selection with IF, ELSE IF, and ELSE
- boolean expressions and range checks
- modules, structured design, and trace tables

You will design loops in pseudocode and flowcharts. You do not need a programming language yet.

## What you will learn

- explain why looping is better than copying the same steps many times
- name and update a loop control variable
- use a priming read before a WHILE loop when input controls the loop
- write the WHILE structure in pseudocode and as a flowchart
- make the loop body move the design toward stopping
- prevent infinite loops with a clear exit condition and a real update

## Why this matters

Many tasks repeat. A cashier adds item prices until the cart is finished. A teacher records attendance for every student. A shopper enters amounts until a total is reached. Writing the same steps twenty times is slow and easy to break. A loop describes the repeating work once and states when to stop.

## 1. Advantages of looping

A **loop** is a structure that repeats a group of steps while a condition remains true, or until a counted pattern is complete.

Benefits:

1. **Less writing.** You describe the repeated work one time.
2. **Easier changes.** Fix the body once, and every repetition improves.
3. **Flexible length.** The same design can run 3 times or 300 times.
4. **Clear stopping rule.** The condition states when repetition ends.

Without a loop, adding five temperatures looks like this:

```text
Input temperature
Set total = total + temperature
Input temperature
Set total = total + temperature
Input temperature
Set total = total + temperature
Input temperature
Set total = total + temperature
Input temperature
Set total = total + temperature
```

With a loop, the pattern is short and can handle any count:

```text
Set count = 1
WHILE count <= 5
    Input temperature
    Set total = total + temperature
    Set count = count + 1
END WHILE
```

## 2. The loop control variable

A **loop control variable** is a value that decides whether the loop continues.

Common kinds:

- a **counter**, such as `count`, that rises or falls each time
- an **input value**, such as `score`, that the user enters each time
- a **flag**, such as `keepGoing`, that becomes false when work is done

The control variable must be:

1. **initialized** before the loop (or primed with a first input)
2. **tested** in the loop condition
3. **updated** inside the loop so the condition can eventually become false

If any of those three pieces is missing, the loop is incomplete.

## 3. WHILE structure in pseudocode

A **WHILE loop** checks a condition before each repetition. If the condition is true, the body runs. If the condition is false, the design skips the body and continues after the loop.

```text
WHILE condition
    statement
    statement
END WHILE
```

Important facts:

- The condition is checked first. If it starts false, the body never runs.
- After the body finishes, the design returns to the condition and checks again.
- The body should change something that affects the condition.

### Simple counter example

```text
Set count = 1

WHILE count <= 3
    Display count
    Set count = count + 1
END WHILE

Display "Done"
```

Trace:

| check | count before body | action | count after update |
| --- | --- | --- | --- |
| 1 <= 3 true | 1 | display 1 | 2 |
| 2 <= 3 true | 2 | display 2 | 3 |
| 3 <= 3 true | 3 | display 3 | 4 |
| 4 <= 3 false | 4 | leave loop | 4 |

Output:

```text
1
2
3
Done
```

## 4. WHILE flowchart

A WHILE loop uses a decision diamond for the condition. One path enters the body. The other path leaves the loop. After the body, a flow line returns to the condition.

```text
                 [Start]
                    |
            Initialize control
                    |
                    v
            +---------------+
       +--->| condition?    |
       |    +-------+-------+
       |       yes /         \ no
       |          /           \
       |     [loop body]      |
       |     update control   |
       |          |           |
       +----------+           v
                         steps after loop
                              |
                           [End]
```

The return arrow is what makes the structure a loop. Without an update to the control value, that arrow becomes a trap.

## 5. Priming read (priming input)

A **priming read** is an input that happens before a WHILE loop so the condition has a value to test.

This pattern is common when the user enters values until a special stop value appears.

Example: add test scores until the user enters -1.

```text
Set total = 0

Input score                // priming read
WHILE score <> -1
    Set total = total + score
    Input score            // update read at the bottom of the loop
END WHILE

Display total
```

Why the first input sits outside:

1. The WHILE condition needs a score before the first check.
2. The body should process only real scores, not the stop value -1.
3. The input at the end of the body prepares the next test.

### Trace with scores 80, 90, -1

| step | score | total | notes |
| --- | --- | --- | --- |
| priming input | 80 | 0 | ready for first check |
| check 80 <> -1 | 80 | 0 | true, enter body |
| add score | 80 | 80 | |
| next input | 90 | 80 | |
| check 90 <> -1 | 90 | 80 | true |
| add score | 90 | 170 | |
| next input | -1 | 170 | |
| check -1 <> -1 | -1 | 170 | false, leave loop |
| display total | -1 | 170 | shows 170 |

The stop value is never added to the total. That is the point of the priming pattern.

## 6. The body must update the control variable

Every useful WHILE loop makes progress toward stopping.

Counter loop progress:

```text
Set count = count + 1
```

or

```text
Set count = count - 1
```

Input loop progress:

```text
Input nextValue
```

Flag loop progress:

```text
Set keepGoing = false
```

If the body never changes the value the condition depends on, the condition stays true forever.

## 7. Infinite loops and how to prevent them

An **infinite loop** repeats without end because the stopping condition never becomes false.

Broken design:

```text
Set count = 1

WHILE count <= 5
    Display count
END WHILE
```

`count` stays 1. The condition stays true. The loop never ends.

Another broken design:

```text
Input score
WHILE score <> -1
    Set total = total + score
END WHILE
```

There is a priming read, but no new input inside the body. The first score is added forever.

### Prevention checklist

Before you finish a WHILE design, ask:

1. What value controls the loop?
2. Where is that value set before the first check?
3. Where does the body change that value?
4. Is there at least one realistic path that makes the condition false?
5. Did I desk-check a short run that actually exits?

## 8. Predict the result

```text
Set n = 4
Set total = 0

WHILE n > 0
    Set total = total + n
    Set n = n - 1
END WHILE

Display total
```

What is displayed?

Work it by hand:

| n before | total before | add | total after | n after |
| --- | --- | --- | --- | --- |
| 4 | 0 | +4 | 4 | 3 |
| 3 | 4 | +3 | 7 | 2 |
| 2 | 7 | +2 | 9 | 1 |
| 1 | 9 | +1 | 10 | 0 |
| 0 | stop |  |  |  |

Displayed result:

```text
10
```

## 9. Worked example: average temperature for a known count

Problem: read 3 daily temperatures and display their average.

```text
Module AverageThreeTemps
    Set count = 1
    Set total = 0

    WHILE count <= 3
        Input temperature
        Set total = total + temperature
        Set count = count + 1
    END WHILE

    Set average = total / 3
    Display average
End Module
```

Trace with inputs 20, 22, 24:

| count check | count | temperature | total after add | count after update |
| --- | --- | --- | --- | --- |
| 1 <= 3 | 1 | 20 | 20 | 2 |
| 2 <= 3 | 2 | 22 | 42 | 3 |
| 3 <= 3 | 3 | 24 | 66 | 4 |
| 4 <= 3 false |  |  | 66 |  |

Average = 66 / 3 = 22.

## 10. Worked example: keep asking until a valid mark

Problem: a mark must be from 0 to 100. Keep asking until the user enters a valid mark.

```text
Module ReadValidMark
    Input mark

    WHILE mark < 0 OR mark > 100
        Display "Mark must be 0 to 100"
        Input mark
    END WHILE

    Display "Accepted"
    Display mark
End Module
```

This uses a priming input and a range check. Invalid values cause another prompt. A valid value ends the loop.

Sample run:

```text
Input: 150
Display: Mark must be 0 to 100
Input: -3
Display: Mark must be 0 to 100
Input: 88
Display: Accepted
Display: 88
```

## 11. WHILE with a running total of prices

Problem: read item prices until the user enters 0. Display the shopping total.

```text
Module ShoppingTotal
    Set total = 0

    Input price
    WHILE price <> 0
        Set total = total + price
        Input price
    END WHILE

    Display total
End Module
```

Flowchart sketch:

```text
              [Start]
                 |
            total = 0
                 |
            Input price   <-----------+
                 |                    |
         +---------------+            |
         | price <> 0 ?  |            |
         +-------+-------+            |
            yes /         \ no        |
               /           \          |
        total = total       |         |
          + price           |         |
               |            |         |
               +------------+----> Display total
                                      |
                                   [End]
```

In a pure WHILE form, the repeated input is usually written at the bottom of the body, with the first input before the loop. Both drawings must preserve the same order of operations.

## 12. Counting how many times the body ran

Sometimes you need both a total and a count of items.

```text
Module CountAndTotal
    Set total = 0
    Set count = 0

    Input value
    WHILE value <> -1
        Set total = total + value
        Set count = count + 1
        Input value
    END WHILE

    Display count
    Display total
End Module
```

Here `value` is the loop control variable for stopping. `count` is a separate counter that records how many real values were processed. Do not confuse the stop condition with the item count unless they are the same thing by design.

## Common mistakes

1. **Forgetting to initialize the control variable.**  
   The first condition test has no known value.

2. **Forgetting to update the control variable.**  
   This is the most common cause of infinite loops.

3. **Using the stop value as real data.**  
   If -1 means "done," do not add -1 into a total. Use a priming read and test before processing.

4. **Off-by-one on counters.**  
   `count < 5` and `count <= 5` are different. Trace the first and last values.

5. **Writing WHILE when the body must always run once first without a condition.**  
   Standard WHILE checks before entry. If you always need one pass first, either restructure with a priming step or use a design that matches that need carefully.

6. **Updating the wrong variable.**  
   The body changes `total` but never changes `count` or the input that the condition uses.

## Check your understanding

1. Name the three jobs a loop control variable must have in a WHILE design.
2. What is a priming read, and why does a sentinel-style input loop need one?
3. Why does this loop never stop?

```text
Set x = 10
WHILE x > 0
    Display x
END WHILE
```

4. In a WHILE flowchart, where does the flow go after the body finishes?
5. How can one design process 2 scores today and 20 scores tomorrow without rewriting the body?

## Practice

Complete the practice tasks in [exercise/exercise.md](./exercise/exercise.md).

Then take the quiz in [quiz/quiz.md](./quiz/quiz.md).

## Next step

Module 15 covers FOR loops, definite loops, and indefinite loops so you can choose the right loop form for counted work and open-ended work.
