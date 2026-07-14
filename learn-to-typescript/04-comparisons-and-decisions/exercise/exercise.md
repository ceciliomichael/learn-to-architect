# Module 04 Exercises

## Warm-up: Compare two numbers

Create `currentPages` with the value `40` and `goalPages` with the value `50`. Print the result of these comparisons:

- current pages are at least the goal
- current pages are less than the goal
- current pages equal `40`

Predict the booleans before running the file.

## Guided exercise: Ticket price

Store a person's age. Print one ticket category:

- under 6: `Free ticket`
- 6 through 17: `Child ticket`
- 18 through 64: `Standard ticket`
- 65 or older: `Senior ticket`

Arrange the checks so every age reaches the correct first match.

## Independent exercise: Study reminder

Create these values:

```typescript
const minutesStudied = 35;
const dailyGoal = 45;
const isRestDay = false;
```

Print exactly one message:

- If it is a rest day, print `Rest and return tomorrow.`
- Otherwise, if the goal is met, print `Daily goal complete.`
- Otherwise, print the number of remaining minutes in a template string.

Change the values to test all three paths.

## Logic exercise

A person may borrow a book when they have a library card and have no overdue book.

Create boolean variables named `hasLibraryCard` and `hasOverdueBook`. Write the condition and test all four possible combinations.

## Debugging task

Correct this program so a score of `92` prints `Excellent`:

```typescript
const score = 92;

if (score >= 60) {
  console.log("Pass");
} else if (score = 90) {
  console.log("Excellent");
} else {
  console.log("Try again");
}
```

## Completion checklist

- [ ] I used strict comparison operators.
- [ ] I tested more than one branch of my code.
- [ ] I ordered numeric ranges correctly.
- [ ] I combined boolean conditions with a clear meaning.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
