# Module 15 Exercises

## Warm-up: Count with FOR

1. Write a FOR loop that displays 1 through 6.
2. Write a FOR loop that displays 10, 8, 6, 4, 2.
3. Predict the values of `n` in `FOR n = 0 TO 12 STEP 4`.

## Guided exercise: Average of four temperatures

Design a module that:

1. Uses a FOR loop to read exactly 4 temperatures.
2. Keeps a running total.
3. Computes and displays the average after the loop.
4. Desk-checks inputs 18, 20, 22, 24. Expected average is 21.
5. Briefly explain why this loop is definite.

## Independent exercise: Choose the right loop

Write two separate designs.

### Design A: Known orders

A bakery must process exactly `orderCount` orders. Input `orderCount`, then for each order input a price and add it to a total. Display the total.

### Design B: Until closed

A cafe adds sale amounts until the cashier enters -1. Display the total of all sales before -1. Do not add -1.

Requirements:

- Choose FOR or WHILE for each design and say why in one sentence.
- Use clear variable names.
- Desk-check Design A with orderCount 3 and prices 2.50, 3.00, 1.75.
- Desk-check Design B with sales 5, 4, 6, -1.

## Debugging / desk-check task

1. This design was meant to display 1, 2, 3, 4, 5. What does it actually do? Fix it.

```text
FOR count = 1 TO 5 STEP 2
    Display count
END FOR
```

2. A learner wrote a FOR loop for scores until -1. Explain why that is the wrong structure and rewrite it correctly with WHILE.

3. Trace this loop and state every value displayed:

```text
FOR n = 5 TO 1 STEP -1
    Display n
END FOR
Display "Go"
```

## Completion checklist

- [ ] I wrote upward and downward FOR loops with correct steps.
- [ ] I designed a definite average with FOR and traced it.
- [ ] I chose FOR and WHILE for two different problems and justified each choice.
- [ ] I fixed step and structure mistakes.
- [ ] I can define definite and indefinite loops in my own words.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
