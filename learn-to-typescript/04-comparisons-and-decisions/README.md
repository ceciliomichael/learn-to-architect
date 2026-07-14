# Module 04: Comparisons and Decisions

## Before you start

Complete Modules 01 to 03. You should be comfortable with variables, strings, numbers, booleans, and basic calculations.

## What you will learn

- create boolean values with comparisons
- compare with strict equality
- choose code with `if`, `else if`, and `else`
- combine conditions with `&&`, `||`, and `!`
- arrange conditions from specific to general

## Why this matters

A program often needs to choose an action. It might show a success message when a goal is met or a reminder when work remains.

## 1. Comparisons produce booleans

```typescript
const score = 80;

console.log(score > 70);
console.log(score === 80);
console.log(score < 50);
```

Expected output:

```text
true
true
false
```

Common comparison operators are:

| Operator | Meaning |
| --- | --- |
| `===` | equal value and equal runtime type |
| `!==` | not equal value or not equal runtime type |
| `>` | greater than |
| `<` | less than |
| `>=` | greater than or equal to |
| `<=` | less than or equal to |

Use `===` and `!==` for equality. JavaScript also has `==` and `!=`, which convert values before comparison. That conversion can be surprising, so this course uses strict equality.

## 2. Run code only when a condition is true

```typescript
const temperature = 31;

if (temperature > 30) {
  console.log("It is a hot day.");
}
```

The expression inside the parentheses is the condition. If it is `true`, the statement inside the braces runs. If it is `false`, that block is skipped.

Indentation shows which statements belong to the block. The braces are what define the block for TypeScript.

## 3. Choose between two paths

```typescript
const hasTicket = false;

if (hasTicket === true) {
  console.log("You may enter.");
} else {
  console.log("A ticket is required.");
}
```

Because `hasTicket` is already a boolean, a shorter condition is also clear:

```typescript
if (hasTicket) {
  console.log("You may enter.");
} else {
  console.log("A ticket is required.");
}
```

Exactly one of these two blocks runs.

## 4. Handle several ranges

```typescript
const score = 76;

if (score >= 90) {
  console.log("Excellent");
} else if (score >= 75) {
  console.log("Good progress");
} else if (score >= 60) {
  console.log("Keep practicing");
} else {
  console.log("Review the lesson");
}
```

The program checks from top to bottom and stops at the first true condition.

Order matters. If `score >= 60` appeared first, a score of `95` would match it before reaching `score >= 90`.

## 5. Combine conditions

The `&&` operator means both sides must be true:

```typescript
const age = 20;
const hasId = true;

if (age >= 18 && hasId) {
  console.log("Entry allowed");
}
```

The `||` operator means at least one side must be true:

```typescript
const isWeekend = false;
const isHoliday = true;

if (isWeekend || isHoliday) {
  console.log("No class today");
}
```

The `!` operator reverses a boolean:

```typescript
const isComplete = false;

if (!isComplete) {
  console.log("Work remains");
}
```

## 6. Store a condition when its meaning deserves a name

```typescript
const balance = 500;
const itemPrice = 320;
const canAffordItem = balance >= itemPrice;

if (canAffordItem) {
  console.log("Purchase is possible");
}
```

The name makes the condition easier to read.

## Predict the result

```typescript
const hoursSlept = 7;
const hasEarlyMeeting = false;

if (hoursSlept >= 8 && !hasEarlyMeeting) {
  console.log("Well rested");
} else if (hoursSlept >= 6) {
  console.log("A reasonable amount of rest");
} else {
  console.log("Rest more when possible");
}
```

Which single message appears, and why?

## Common mistakes

### Using `=` instead of `===`

`=` assigns. `===` compares. An `if` condition normally needs a comparison or an existing boolean value.

### Writing overlapping ranges in the wrong order

Check the most specific or highest threshold first.

### Forgetting braces

Always use braces in this course. They make the controlled block clear.

### Making one condition too complicated

Give important pieces descriptive boolean names, then combine those names.

## Check your understanding

1. What type does a comparison produce?
2. Why does this course use `===` instead of `==`?
3. When does an `else` block run?
4. What is the difference between `&&` and `||`?
5. Why should a high score threshold come before a lower one?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 05](../05-repeating-work-with-loops/README.md) teaches how to repeat an action without copying the same statement many times.
