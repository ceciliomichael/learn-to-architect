# Module 05: Repeating Work with Loops

## Before you start

Complete Modules 01 to 04. You should understand variables, arithmetic, comparisons, and `if` statements.

## What you will learn

- recognize work that can be repeated
- write a counted `for` loop
- write a condition-controlled `while` loop
- update a running total
- stop a loop with `break`
- prevent common infinite loops

## Why this matters

Copying the same instruction many times is slow and easy to get wrong. A loop describes what repeats and when the repetition should stop.

## 1. A counted `for` loop

This loop prints the numbers 1 through 5:

```typescript
for (let count = 1; count <= 5; count = count + 1) {
  console.log(count);
}
```

The parentheses contain three parts:

1. `let count = 1` runs once before the loop begins.
2. `count <= 5` is checked before each repetition.
3. `count = count + 1` runs after each repetition.

The statements inside the braces are the loop body.

## 2. Trace a loop by hand

For the first repetition:

- `count` starts at `1`.
- `1 <= 5` is true.
- The program prints `1`.
- The update changes `count` to `2`.

This continues until `count` becomes `6`. The condition `6 <= 5` is false, so the loop stops.

Tracing means writing down how values change. It is one of the most useful debugging habits.

## 3. Count down

```typescript
for (let number = 3; number >= 1; number = number - 1) {
  console.log(number);
}

console.log("Go!");
```

Expected output:

```text
3
2
1
Go!
```

The final statement is outside the loop, so it runs once after the loop ends.

## 4. Build a running total

```typescript
let total = 0;

for (let number = 1; number <= 4; number = number + 1) {
  total = total + number;
}

console.log(total);
```

The total changes like this:

| number | total after addition |
| --- | --- |
| 1 | 1 |
| 2 | 3 |
| 3 | 6 |
| 4 | 10 |

The total is created before the loop because its final value is needed afterward.

## 5. Use `while` when the condition is the main idea

```typescript
let battery = 3;

while (battery > 0) {
  console.log(`Battery level: ${battery}`);
  battery = battery - 1;
}

console.log("Battery empty");
```

A `while` loop continues as long as its condition is true. The loop body must make progress toward making the condition false.

Use a `for` loop when you have a clear counter. Use a `while` loop when repetition is best described by a condition.

## 6. Skip or stop based on a decision

`continue` skips the rest of the current repetition:

```typescript
for (let number = 1; number <= 5; number = number + 1) {
  if (number === 3) {
    continue;
  }

  console.log(number);
}
```

`break` stops the whole loop:

```typescript
for (let attempt = 1; attempt <= 5; attempt = attempt + 1) {
  console.log(`Attempt ${attempt}`);

  if (attempt === 3) {
    break;
  }
}
```

Use both sparingly. A simple loop condition is often easier to read.

## 7. Infinite loops

This loop never changes `count`, so its condition stays true:

```typescript
let count = 1;

// Intentional problem: do not run this loop.
while (count <= 5) {
  console.log(count);
}
```

The fix is to update `count` inside the loop:

```typescript
count = count + 1;
```

If a program prints endlessly, stop it in the terminal with Ctrl+C. Then check the loop condition and updates.

## Predict the result

```typescript
let result = 1;

for (let step = 1; step <= 3; step = step + 1) {
  result = result * 2;
  console.log(result);
}
```

Trace `step` and `result` for each repetition before running the file.

## Common mistakes

### Starting or ending one step too early

Write down the first and last desired values. Check both boundaries.

### Updating in the wrong direction

If a condition is `count <= 5`, subtracting from `count` moves away from the stopping point.

### Creating a running total inside the loop

That would reset it on every repetition. Create it before the loop.

### Changing the wrong variable

Trace the condition variable after one repetition. It should move closer to stopping.

## Check your understanding

1. What are the three parts of the shown `for` loop?
2. When is a `while` loop a natural choice?
3. Why must the loop body make progress?
4. What is the difference between `continue` and `break`?
5. Where should a running total be created?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 06](../06-functions/README.md) teaches how to name a group of steps and use it more than once.
