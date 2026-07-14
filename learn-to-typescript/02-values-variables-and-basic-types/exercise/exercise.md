# Module 02 Exercises

## Warm-up: Describe a book

Create three variables:

- a constant named `bookTitle` containing a string
- a constant named `pageCount` containing a number
- a constant named `isFinished` containing a boolean

Print each value. Then print the result of `typeof` for each value.

## Guided exercise: Track study minutes

1. Create `studyMinutes` with `let` and the value `20`.
2. Print it.
3. Assign `35` to the same variable.
4. Print it again.
5. Create a constant named `subject` with the value `"TypeScript"`.
6. Print `subject`.

Expected output:

```text
20
35
TypeScript
```

## Independent exercise: Simple profile data

Create and print values for:

- a display name
- a year of birth
- whether the person likes puzzles
- a score that begins at `0` and later changes to `10`

Use `const` wherever reassignment is not needed. Use `let` for the score.

## Debugging task

Correct every line that causes a type or assignment error:

```typescript
const city = "Cebu";
city = "Davao";

let visitCount = 1;
visitCount = "two";

const isSunny = "true";
console.log(typeof isSunny);
```

The corrected program should store:

- one city that does not change
- a visit count that changes from `1` to `2`
- a real boolean value for the weather

## Completion checklist

- [ ] I used `const` for values that did not need reassignment.
- [ ] I used `let` for a value that changed.
- [ ] I kept strings, numbers, and booleans distinct.
- [ ] I used `typeof` and understood its output.

Compare your work with the [exercise solutions](../answers/exercise/exercise-solutions.md) after attempting every task.
