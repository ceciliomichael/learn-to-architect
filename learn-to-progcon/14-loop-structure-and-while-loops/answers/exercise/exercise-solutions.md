# Module 14 Exercise Solutions

## Warm-up solution

```text
Set count = 1

WHILE count <= 4
    Display count
    Set count = count + 1
END WHILE

Display "Finished"
```

Trace:

| condition | count | display | count after update |
| --- | --- | --- | --- |
| 1 <= 4 true | 1 | 1 | 2 |
| 2 <= 4 true | 2 | 2 | 3 |
| 3 <= 4 true | 3 | 3 | 4 |
| 4 <= 4 true | 4 | 4 | 5 |
| 5 <= 4 false | 5 | leave loop |  |

Output:

```text
1
2
3
4
Finished
```

## Guided exercise solution

```text
Module SumUntilZero
    Set total = 0

    Input number
    WHILE number <> 0
        Set total = total + number
        Input number
    END WHILE

    Display total
End Module
```

Desk check for 4, 6, 5, 0:

| step | number | total | notes |
| --- | --- | --- | --- |
| priming input | 4 | 0 | |
| check, add | 4 | 4 | 4 <> 0 |
| input | 6 | 4 | |
| check, add | 6 | 10 | |
| input | 5 | 10 | |
| check, add | 5 | 15 | |
| input | 0 | 15 | |
| check | 0 | 15 | 0 <> 0 is false |

Displayed total:

```text
15
```

Zero is the stop value, so it is never added.

## Independent exercise solution

```text
Module AttendanceCounter
    Set count = 0

    Input name
    WHILE name <> "STOP"
        Set count = count + 1
        Input name
    END WHILE

    Display count
End Module
```

A message form is also fine:

```text
Display "Members: "
Display count
```

Text flowchart:

```text
                 [Start]
                    |
               count = 0
                    |
               Input name  <-----------+
                    |                  |
            +---------------+          |
            | name <> STOP? |          |
            +-------+-------+          |
               yes /         \ no      |
                  /           \        |
           count = count       |       |
              + 1              |       |
                  |            |       |
                  +------------+       |
                         |             |
                         +-------------+
                         |
                   Display count
                         |
                      [End]
```

Desk check for Ana, Ben, Cam, STOP:

| name | count after processing |
| --- | --- |
| Ana | 1 |
| Ben | 2 |
| Cam | 3 |
| STOP | loop ends, count stays 3 |

Expected display:

```text
3
```

## Debugging / desk-check task solution

1. The first design never changes `n`. The condition `n > 0` stays true, so the loop is infinite.
2. Correct countdown:

```text
Set n = 5

WHILE n > 0
    Display n
    Set n = n - 1
END WHILE

Display "Lift off"
```

3. Trace of the fixed version:

| n before | display | n after |
| --- | --- | --- |
| 5 | 5 | 4 |
| 4 | 4 | 3 |
| 3 | 3 | 2 |
| 2 | 2 | 1 |
| 1 | 1 | 0 |
| 0 | leave loop |  |

Output:

```text
5
4
3
2
1
Lift off
```

4. Second bug: `Set n = n + 1` makes `n` grow: 5, 6, 7, ... The condition `n > 0` stays true forever. Correct update for a countdown is `Set n = n - 1`.
