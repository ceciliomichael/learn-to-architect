# Module 05 Exercises

## Warm-up: Count by twos

Write a `for` loop that prints:

```text
2
4
6
8
10
```

Update the counter by `2` each time.

## Guided exercise: Add a range

Use a loop to add all whole numbers from 1 through 10.

1. Create `total` with the value `0` before the loop.
2. Create a `for` loop whose counter begins at `1` and ends at `10`.
3. Add the counter to `total` during each repetition.
4. Print only the final total after the loop.

Expected output:

```text
55
```

## Independent exercise: Multiplication table

Create a constant named `baseNumber` with the value `4`. Use a loop to print:

```text
4 x 1 = 4
4 x 2 = 8
4 x 3 = 12
4 x 4 = 16
4 x 5 = 20
```

Calculate every result. Use a template string for each line.

## While exercise: Countdown

Use a `while` loop to print `5` down to `1`, then print `Finished` once after the loop.

## Debugging task

This program should print `1`, `2`, and `3`, then stop. Fix it.

```typescript
let count = 1;

while (count <= 3) {
  console.log(count);
  count = count - 1;
}
```

Explain why the original loop did not stop.

## Completion checklist

- [ ] I traced at least one loop on paper.
- [ ] My counter reached both intended boundaries.
- [ ] I kept a running total outside the loop.
- [ ] My `while` loop moved toward a false condition.

Then compare with the [exercise solutions](../answers/exercise/exercise-solutions.md).
