# Module 13: Range Checks and Nested Decisions

## Before you start

Complete Modules 01 to 12. You should already know:

- single-alternative and dual-alternative selection
- boolean expressions and truth values
- relational operators such as `>=`, `<=`, `>`, `<`, and `=`
- logical operators AND, OR, and NOT
- modules, structured design, and trace tables

You will design with pseudocode and flowcharts. You do not need a programming language for this module.

## What you will learn

- check whether a value sits between a low and a high limit
- write multi-way selection with ELSE IF chains
- nest decisions carefully when one choice depends on another
- put conditions in the right order so the first true branch is the correct branch
- prefer a clear multi-way structure when deep nesting only adds confusion

## Why this matters

Real problems often have more than two outcomes. A test score becomes a letter grade. An age becomes a ticket price. A package weight becomes a shipping cost. You need a reliable way to sort a value into the right band without missing cases or double-counting them.

## 1. A range check tests a band of values

A **range check** tests whether a value is between two limits.

A common form uses AND:

```text
IF temperature >= 18 AND temperature <= 24 THEN
    Display "Comfortable room"
END IF
```

Both sides must be true. The temperature must be at least 18 and at most 24.

Say the words out loud when you write the test: "at least low and at most high."

| temperature | temperature >= 18 | temperature <= 24 | whole condition |
| --- | --- | --- | --- |
| 15 | false | true | false |
| 18 | true | true | true |
| 22 | true | true | true |
| 24 | true | true | true |
| 30 | true | false | false |

### Inclusive and exclusive ends

**Inclusive** means the endpoint counts. The checks `>=` and `<=` are inclusive.

**Exclusive** means the endpoint does not count. The checks `>` and `<` are exclusive.

Examples:

- ages 13 through 17 inclusive: `age >= 13 AND age <= 17`
- scores above 0 and below 100 exclusive of both ends: `score > 0 AND score < 100`
- prices from 10 up to but not including 20: `price >= 10 AND price < 20`

Write the rule in plain English first. Then choose operators that match the English exactly.

## 2. Predict the result: one range

```text
Set score = 75
IF score >= 70 AND score <= 79 THEN
    Display "Band: C"
END IF
```

What is displayed?

Answer after you try:

```text
Band: C
```

Score 75 is at least 70 and at most 79, so the condition is true.

## 3. Multi-way selection: more than two paths

A **multi-way selection** chooses one path among several related options.

In pseudocode, use ELSE IF for each middle band, and ELSE for everything left:

```text
IF score >= 90 THEN
    Set grade = "A"
ELSE IF score >= 80 THEN
    Set grade = "B"
ELSE IF score >= 70 THEN
    Set grade = "C"
ELSE IF score >= 60 THEN
    Set grade = "D"
ELSE
    Set grade = "F"
END IF
```

The computer checks conditions from top to bottom. It runs the first true branch, then skips the rest.

That order matters. When the program reaches `score >= 80`, it already knows the score is less than 90. Each later condition only needs the next lower boundary.

### Flowchart of a multi-way grade band

```text
                 [Start]
                    |
              Input score
                    |
            +---------------+
            | score >= 90?  |
            +-------+-------+
               yes /         \ no
                  /           \
           grade = "A"   +---------------+
                  |      | score >= 80?  |
                  |      +-------+-------+
                  |         yes /         \ no
                  |            /           \
                  |     grade = "B"  +---------------+
                  |            |     | score >= 70?  |
                  |            |     +-------+-------+
                  |            |        yes /         \ no
                  |            |           /           \
                  |            |    grade = "C"   (continue for
                  |            |           |       D and F)
                  +------+-----+-----------+
                         |
                   Display grade
                         |
                      [End]
```

Each diamond is one question. Exactly one grade assignment runs for a given score.

## 4. Order of conditions decides which branch wins

Compare these two designs for the same score of 95.

Wrong order:

```text
IF score >= 60 THEN
    Display "Pass"
ELSE IF score >= 90 THEN
    Display "Excellent"
END IF
```

Result for 95:

```text
Pass
```

Score 95 is already greater than or equal to 60, so the first branch runs. The "Excellent" branch never runs.

Right order for highest band first:

```text
IF score >= 90 THEN
    Display "Excellent"
ELSE IF score >= 60 THEN
    Display "Pass"
ELSE
    Display "Needs work"
END IF
```

Result for 95:

```text
Excellent
```

Rule of thumb for related numeric bands:

1. Put the most specific or highest threshold first when you use "at least" checks from the top.
2. Or write full range checks for every band so each band stands alone.

Both styles work when they are consistent.

### Full range form

```text
IF score >= 90 AND score <= 100 THEN
    Set grade = "A"
ELSE IF score >= 80 AND score <= 89 THEN
    Set grade = "B"
ELSE IF score >= 70 AND score <= 79 THEN
    Set grade = "C"
ELSE IF score >= 60 AND score <= 69 THEN
    Set grade = "D"
ELSE IF score >= 0 AND score <= 59 THEN
    Set grade = "F"
ELSE
    Display "Score out of range"
END IF
```

This form is longer. It makes each band explicit and catches invalid scores in the ELSE.

## 5. Nested decisions: a choice inside a choice

A **nested decision** places one IF inside another IF.

Use nesting when the second question only makes sense after the first answer is true.

Example: store entry, then ticket type.

```text
IF hasTicket = true THEN
    IF age < 13 THEN
        Display "Child seat area"
    ELSE
        Display "General seating"
    END IF
ELSE
    Display "Ticket required"
END IF
```

Reading order:

1. First check the ticket.
2. Only if the ticket is present, check age.
3. If there is no ticket, age does not matter for seating.

### When nesting is the right tool

Nest when:

- one rule depends on another being true
- a second question would be meaningless on the other path
- you must handle a special case before a general case that itself has sub-cases

Example with discounts:

```text
IF isMember = true THEN
    IF cartTotal >= 50 THEN
        Set discount = 0.15
    ELSE
        Set discount = 0.05
    END IF
ELSE
    Set discount = 0
END IF
```

Non-members never get a member discount. The cart total only matters for members.

## 6. Nested decisions can become hard to read

Deep nesting means IF inside IF inside IF. After two or three levels, most people lose track of which ELSE belongs to which IF.

Hard to follow:

```text
IF dayType = "weekday" THEN
    IF timeOfDay = "morning" THEN
        IF isHoliday = false THEN
            Display "Peak fare"
        ELSE
            Display "Holiday fare"
        END IF
    ELSE
        Display "Off-peak weekday fare"
    END IF
ELSE
    Display "Weekend fare"
END IF
```

Clearer multi-way style for the same idea:

```text
IF dayType = "weekend" THEN
    Display "Weekend fare"
ELSE IF isHoliday = true THEN
    Display "Holiday fare"
ELSE IF timeOfDay = "morning" THEN
    Display "Peak fare"
ELSE
    Display "Off-peak weekday fare"
END IF
```

The multi-way form still has order rules. Weekend and holiday are handled before the weekday morning test.

Guideline:

- Prefer multi-way selection for one value sorted into bands.
- Prefer nesting when a later question only applies on one earlier path.
- If you need more than two nested levels, stop and redesign with modules or clearer multi-way checks.

## 7. Worked example: age groups

Problem: assign an age group for a community class list.

Rules:

- under 13: Child
- 13 through 17: Teen
- 18 through 64: Adult
- 65 and older: Senior
- age less than 0: Invalid

Pseudocode:

```text
Module AssignAgeGroup
    Input age

    IF age < 0 THEN
        Set group = "Invalid"
    ELSE IF age < 13 THEN
        Set group = "Child"
    ELSE IF age < 18 THEN
        Set group = "Teen"
    ELSE IF age < 65 THEN
        Set group = "Adult"
    ELSE
        Set group = "Senior"
    END IF

    Display group
End Module
```

After each true branch, the remaining code already knows lower bounds failed. Age 20 is not less than 0, not less than 13, not less than 18, and is less than 65, so the group is Adult.

### Trace table for ages 10, 15, 40, 70

| age | age < 0 | age < 13 | age < 18 | age < 65 | group |
| --- | --- | --- | --- | --- | --- |
| 10 | false | true | (skipped) | (skipped) | Child |
| 15 | false | false | true | (skipped) | Teen |
| 40 | false | false | false | true | Adult |
| 70 | false | false | false | false | Senior |

## 8. Worked example: shipping tiers

Problem: choose a shipping cost from package weight in kilograms.

Rules:

- weight less than or equal to 0: invalid
- up to 1 kg: 5.00
- more than 1 kg up to 5 kg: 8.50
- more than 5 kg up to 20 kg: 15.00
- more than 20 kg: 25.00

```text
Module ShippingCost
    Input weight

    IF weight <= 0 THEN
        Display "Invalid weight"
    ELSE IF weight <= 1 THEN
        Set cost = 5.00
        Display cost
    ELSE IF weight <= 5 THEN
        Set cost = 8.50
        Display cost
    ELSE IF weight <= 20 THEN
        Set cost = 15.00
        Display cost
    ELSE
        Set cost = 25.00
        Display cost
    END IF
End Module
```

Because the chain moves upward with "at most" checks, each later branch already excludes lighter packages.

### Predict the result

What does the design display for weight 5?

Answer:

```text
8.5
```

(or 8.50, depending on how you write the number)

Weight 5 is greater than 1, so the second shipping band fails. Weight 5 is less than or equal to 5, so the third band runs.

What does it display for weight 0?

```text
Invalid weight
```

## 9. Worked example: nested rule with a range inside

Problem: temperature alert for a fridge.

Rules:

- If the sensor is offline, display "No reading".
- If the sensor is online and temperature is between 1 and 4 inclusive, display "Safe".
- If the sensor is online and temperature is outside that range, display "Check fridge".

```text
Module FridgeAlert
    Input sensorOnline
    Input temperature

    IF sensorOnline = false THEN
        Display "No reading"
    ELSE
        IF temperature >= 1 AND temperature <= 4 THEN
            Display "Safe"
        ELSE
            Display "Check fridge"
        END IF
    END IF
End Module
```

The range check only runs when a reading exists. That is a good use of nesting.

A multi-way rewrite is possible with compound conditions:

```text
IF sensorOnline = false THEN
    Display "No reading"
ELSE IF temperature >= 1 AND temperature <= 4 THEN
    Display "Safe"
ELSE
    Display "Check fridge"
END IF
```

Both designs are valid. Choose the form that is easier to read for the problem.

## 10. Boundary values deserve extra desk checks

Boundaries are the numbers on the edge of a rule: the lowest accepted value, the highest accepted value, and the values just outside.

For grades that use `score >= 90` for an A, test at least:

- 89
- 90
- 100
- a value below 0 if invalid scores are possible

For a range `age >= 13 AND age <= 17`, test:

- 12
- 13
- 17
- 18

If the wrong band wins on a boundary, fix the operators or the order before you write more cases.

## Common mistakes

1. **Wrong inclusive or exclusive choice.**  
   "Ages 13 to 17" usually includes 13 and 17. Use `>=` and `<=`, not `>` and `<`, unless the rule says otherwise.

2. **Putting a broad condition before a narrow one.**  
   `score >= 60` before `score >= 90` steals high scores.

3. **Using OR when you meant AND in a range.**  
   `score >= 70 OR score <= 79` is true for almost every number. A range needs AND.

4. **Forgetting an ELSE for leftover cases.**  
   Without a final ELSE, invalid or unexpected values may produce no message at all.

5. **Nesting when a multi-way chain is clearer.**  
   Deep nests hide which ELSE matches which IF. Prefer ELSE IF for bands of one value.

6. **Overlapping bands that both look true.**  
   If you write full ranges, keep them disjoint: 80-89 and 90-100, not 80-90 and 90-100, unless you want 90 claimed by the first match only.

## Check your understanding

1. Write a condition that is true when `price` is from 10 to 25 inclusive.
2. Why does checking `score >= 60` before `score >= 90` cause wrong messages for high scores?
3. When is a nested IF better than a flat ELSE IF chain?
4. For shipping tiers that use rising weight limits, why can later conditions skip the lower bound?
5. Which operators make a range exclusive on both ends?

## Practice

Complete the practice tasks in [exercise/exercise.md](./exercise/exercise.md).

Then take the quiz in [quiz/quiz.md](./quiz/quiz.md).

## Next step

Module 14 introduces loop structure and WHILE loops so a design can repeat work until a condition becomes false.
