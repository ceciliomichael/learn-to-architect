# Module 16 Exercises

## Warm-up: Seat map counts

A small theater has 2 rows and 5 seats in each row.

1. Write nested FOR loops that display every row and seat pair.
2. State how many pairs are displayed.
3. Change the design so it only counts the seats into `seatTotal` and displays that total once at the end. Expected total is 10.

## Guided exercise: Totals with a sentinel

Design a module that:

1. Reads item prices until the user enters -1.
2. Accumulates a total of valid prices.
3. Counts how many items were purchased.
4. Displays the item count and the total.
5. Rejects negative prices other than the sentinel without ending the loop. (If a negative value other than -1 appears, display a warning and continue.)
6. Desk-checks this sequence: 4.50, -3, 2.00, 1.50, -1.

Expected processed items: 3. Expected total: 8.00.

## Independent exercise: Nested class scores

A workshop has 3 teams. Each team has 4 scores.

Requirements:

- Use nested loops.
- For each team, read 4 scores, compute the team total, and display the team number and team total.
- Also keep a grand total of every score and display it after all teams.
- Reset each team total at the correct time.
- Desk-check with these scores:
  - Team 1: 2, 3, 4, 5
  - Team 2: 1, 1, 1, 1
  - Team 3: 5, 5, 5, 5
- Expected team totals: 14, 4, 20. Expected grand total: 38.

## Debugging / desk-check task

### Bug 1

This design was meant to sum scores until -1. Trace it with inputs 10, 20, -1 and explain the failure. Then rewrite it correctly.

```text
Set total = 0
Input score
WHILE score = -1
    Set total = total + score
    Input score
END WHILE
Display total
```

### Bug 2

This nested design reuses one counter. Explain the problem and rewrite it with clear names.

```text
FOR i = 1 TO 2
    FOR i = 1 TO 3
        Display i
    END FOR
END FOR
```

### Bug 3

This class total design forgets to reset. Desk-check teams with scores (1, 1) and (2, 2) using 2 teams of 2 scores each. Show why the second total is wrong, then fix the design.

```text
Set teamTotal = 0
FOR team = 1 TO 2
    FOR scoreNumber = 1 TO 2
        Input score
        Set teamTotal = teamTotal + score
    END FOR
    Display teamTotal
END FOR
```

## Completion checklist

- [ ] I wrote nested loops for a seat map and counted the repetitions.
- [ ] I designed sentinel input with a count, a total, and invalid-value handling.
- [ ] I built a nested team-score design with correct resets and a grand total.
- [ ] I diagnosed wrong conditions, reused counters, and missing resets.
- [ ] I can explain counters, accumulators, and sentinels with examples.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
