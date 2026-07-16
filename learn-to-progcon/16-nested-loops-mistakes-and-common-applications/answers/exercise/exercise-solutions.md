# Module 16 Exercise Solutions

## Warm-up solution

1. Display every pair:

```text
FOR row = 1 TO 2
    FOR seat = 1 TO 5
        Display row
        Display seat
    END FOR
END FOR
```

2. Number of pairs: 2 * 5 = 10.

3. Count only:

```text
Set seatTotal = 0

FOR row = 1 TO 2
    FOR seat = 1 TO 5
        Set seatTotal = seatTotal + 1
    END FOR
END FOR

Display seatTotal
```

Expected display:

```text
10
```

## Guided exercise solution

```text
Module PriceSummary
    Set total = 0
    Set itemCount = 0

    Display "Enter price, or -1 to finish"
    Input price

    WHILE price <> -1
        IF price < 0 THEN
            Display "Price must be zero or positive, or -1 to finish"
        ELSE
            Set total = total + price
            Set itemCount = itemCount + 1
        END IF
        Input price
    END WHILE

    Display itemCount
    Display total
End Module
```

If free items with price 0 should not count as purchases, tighten the valid branch to `price > 0`. For this solution, 0 is treated as a valid free item and is counted.

Desk check for 4.50, -3, 2.00, 1.50, -1:

| price | action | itemCount | total |
| --- | --- | --- | --- |
| 4.50 | add | 1 | 4.50 |
| -3 | warning only | 1 | 4.50 |
| 2.00 | add | 2 | 6.50 |
| 1.50 | add | 3 | 8.00 |
| -1 | end loop | 3 | 8.00 |

Expected displays: item count 3, total 8.00.

## Independent exercise solution

```text
Module WorkshopTeams
    Set grandTotal = 0

    FOR team = 1 TO 3
        Set teamTotal = 0

        FOR scoreNumber = 1 TO 4
            Input score
            Set teamTotal = teamTotal + score
            Set grandTotal = grandTotal + score
        END FOR

        Display team
        Display teamTotal
    END FOR

    Display grandTotal
End Module
```

Desk check:

| team | scores | teamTotal | grandTotal after team |
| --- | --- | --- | --- |
| 1 | 2, 3, 4, 5 | 14 | 14 |
| 2 | 1, 1, 1, 1 | 4 | 18 |
| 3 | 5, 5, 5, 5 | 20 | 38 |

Displays:

```text
1
14
2
4
3
20
38
```

`teamTotal` is set to 0 at the start of each outer pass so team results stay separate. `grandTotal` is initialized once before the outer loop.

## Debugging / desk-check task solution

### Bug 1

With inputs 10, 20, -1:

- priming score is 10
- condition `score = -1` is false
- body never runs
- displayed total is 0

The condition uses equality to the sentinel instead of inequality. Correct structure:

```text
Set total = 0
Input score
WHILE score <> -1
    Set total = total + score
    Input score
END WHILE
Display total
```

Trace with 10, 20, -1:

| score | total after body |
| --- | --- |
| 10 | 10 |
| 20 | 30 |
| -1 | leave loop |

Displayed total: 30.

### Bug 2

Both loops use `i`. The inner loop overwrites the outer counter, so outer control is no longer reliable.

Rewrite:

```text
FOR row = 1 TO 2
    FOR col = 1 TO 3
        Display row
        Display col
    END FOR
END FOR
```

### Bug 3

Broken design desk check with scores 1, 1 then 2, 2:

| team | scores added | teamTotal displayed |
| --- | --- | --- |
| 1 | 1 + 1 | 2 |
| 2 | continues from 2, then +2 +2 | 6 |

Team 2 should total 4, not 6. The accumulator was not reset.

Fixed design:

```text
FOR team = 1 TO 2
    Set teamTotal = 0
    FOR scoreNumber = 1 TO 2
        Input score
        Set teamTotal = teamTotal + score
    END FOR
    Display teamTotal
END FOR
```

Correct displays: 2 then 4.
