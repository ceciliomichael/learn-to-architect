# Module 15 Exercise Solutions

## Warm-up solution

1. Count 1 through 6:

```text
FOR n = 1 TO 6
    Display n
END FOR
```

2. Count down by 2 from 10 to 2:

```text
FOR n = 10 TO 2 STEP -2
    Display n
END FOR
```

3. Values of `n` for `FOR n = 0 TO 12 STEP 4`:

```text
0, 4, 8, 12
```

## Guided exercise solution

```text
Module AverageFourTemps
    Set total = 0

    FOR i = 1 TO 4
        Input temperature
        Set total = total + temperature
    END FOR

    Set average = total / 4
    Display average
End Module
```

Desk check for 18, 20, 22, 24:

| i | temperature | total |
| --- | --- | --- |
| 1 | 18 | 18 |
| 2 | 20 | 38 |
| 3 | 22 | 60 |
| 4 | 24 | 84 |

Average = 84 / 4 = 21.

Displayed result:

```text
21
```

The loop is definite because it always runs exactly four times. The count is known before the loop starts.

## Independent exercise solution

### Design A

FOR is best because the number of orders is known once `orderCount` is entered.

```text
Module KnownOrders
    Input orderCount
    Set total = 0

    FOR i = 1 TO orderCount
        Input price
        Set total = total + price
    END FOR

    Display total
End Module
```

Desk check: orderCount 3, prices 2.50, 3.00, 1.75.

| i | price | total |
| --- | --- | --- |
| 1 | 2.50 | 2.50 |
| 2 | 3.00 | 5.50 |
| 3 | 1.75 | 7.25 |

Displayed total:

```text
7.25
```

### Design B

WHILE is best because the number of sales is unknown. The cashier stops with the sentinel -1.

```text
Module SalesUntilClosed
    Set total = 0

    Input sale
    WHILE sale <> -1
        Set total = total + sale
        Input sale
    END WHILE

    Display total
End Module
```

Desk check: 5, 4, 6, -1.

| sale | total after processing |
| --- | --- |
| 5 | 5 |
| 4 | 9 |
| 6 | 15 |
| -1 | loop ends, total stays 15 |

Displayed total:

```text
15
```

## Debugging / desk-check task solution

1. With STEP 2, the original design displays:

```text
1
3
5
```

It skips the even numbers. Fixed design for 1 through 5:

```text
FOR count = 1 TO 5 STEP 1
    Display count
END FOR
```

or simply:

```text
FOR count = 1 TO 5
    Display count
END FOR
```

2. Scores until -1 are indefinite. A FOR loop needs a known count. Correct WHILE form:

```text
Set total = 0

Input score
WHILE score <> -1
    Set total = total + score
    Input score
END WHILE

Display total
```

3. Trace of the countdown:

| n | display |
| --- | --- |
| 5 | 5 |
| 4 | 4 |
| 3 | 3 |
| 2 | 2 |
| 1 | 1 |
| after loop | Go |

Full output:

```text
5
4
3
2
1
Go
```
