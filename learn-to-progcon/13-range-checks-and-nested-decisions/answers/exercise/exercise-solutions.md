# Module 13 Exercise Solutions

## Warm-up solution

Condition:

```text
temperature >= 18 AND temperature <= 24
```

Predictions:

| temperature | result |
| --- | --- |
| 17 | false |
| 18 | true |
| 21 | true |
| 24 | true |
| 25 | false |

Selection:

```text
IF temperature >= 18 AND temperature <= 24 THEN
    Display "Comfortable"
ELSE
    Display "Adjust climate"
END IF
```

Both limits are inclusive, so 18 and 24 count as comfortable.

## Guided exercise solution

Plain English order:

1. If the score is 90 to 100, grade is A.
2. Else if the score is 80 to 89, grade is B.
3. Else if the score is 70 to 79, grade is C.
4. Else if the score is 60 to 69, grade is D.
5. Else if the score is 0 to 59, grade is F.
6. Else the score is invalid.

Pseudocode:

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
    Set grade = "Invalid"
END IF

Display grade
```

Trace table:

| score | grade |
| --- | --- |
| 95 | A |
| 80 | B |
| 72 | C |
| 60 | D |
| 40 | F |
| 105 | Invalid |

An equivalent shorter chain that assumes scores are already known to be 0 to 100:

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

That shorter form does not catch 105 as Invalid unless you add a separate range check first.

## Independent exercise solution

```text
Module BusTicketPrice
    Input age

    IF age < 0 THEN
        Display "Invalid age"
    ELSE IF age <= 4 THEN
        Set price = 0
        Display price
    ELSE IF age <= 17 THEN
        Set price = 1.50
        Display price
    ELSE IF age <= 64 THEN
        Set price = 2.75
        Display price
    ELSE
        Set price = 1.25
        Display price
    END IF
End Module
```

Text flowchart:

```text
                 [Start]
                    |
                Input age
                    |
            +---------------+
            |   age < 0 ?   |
            +-------+-------+
               yes /         \ no
                  /           \
        "Invalid age"   +---------------+
                  |     |  age <= 4 ?   |
                  |     +-------+-------+
                  |        yes /         \ no
                  |           /           \
                  |     price = 0   +---------------+
                  |           |     | age <= 17 ?   |
                  |           |     +-------+-------+
                  |           |        yes /         \ no
                  |           |           /           \
                  |           |   price = 1.50  +---------------+
                  |           |           |     | age <= 64 ?   |
                  |           |           |     +-------+-------+
                  |           |           |        yes /         \ no
                  |           |           |           /           \
                  |           |           |   price = 2.75  price = 1.25
                  |           |           |           |           |
                  +-----------+-----------+-----------+-----------+
                                      |
                               Display price
                               (or error already shown)
                                      |
                                   [End]
```

Desk check:

| age | result |
| --- | --- |
| -1 | Invalid age |
| 3 | 0 |
| 12 | 1.50 |
| 30 | 2.75 |
| 70 | 1.25 |

## Debugging / desk-check task solution

1. For score 92, `score >= 60` is true, so the design displays `Pass`.
2. "Excellent" never runs because the first true branch ends the multi-way selection. Score 92 already satisfies the broad pass test.
3. Corrected order:

```text
Set score = 92

IF score >= 90 THEN
    Display "Excellent"
ELSE IF score >= 60 THEN
    Display "Pass"
ELSE
    Display "Needs work"
END IF
```

Expected results:

| score | display |
| --- | --- |
| 92 | Excellent |
| 75 | Pass |
| 50 | Needs work |

4. Full range alternative:

```text
IF score < 0 OR score > 100 THEN
    Display "Out of range"
ELSE IF score >= 90 THEN
    Display "Excellent"
ELSE IF score >= 60 THEN
    Display "Pass"
ELSE
    Display "Needs work"
END IF
```

The invalid check comes first so impossible scores are not labeled as Pass or Excellent.
