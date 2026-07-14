# Module 02 Exercise Solutions

## Warm-up solution

```typescript
const bookTitle = "The Secret Garden";
const pageCount = 331;
const isFinished = false;

console.log(bookTitle);
console.log(pageCount);
console.log(isFinished);

console.log(typeof bookTitle);
console.log(typeof pageCount);
console.log(typeof isFinished);
```

Expected final three lines:

```text
string
number
boolean
```

Your book information may differ. The types should match the meanings.

## Guided exercise solution

```typescript
let studyMinutes = 20;
console.log(studyMinutes);

studyMinutes = 35;
console.log(studyMinutes);

const subject = "TypeScript";
console.log(subject);
```

`studyMinutes` uses `let` because it receives a new value. `subject` uses `const` because it does not change.

## Independent exercise solution

```typescript
const displayName = "Kai";
const birthYear = 2001;
const likesPuzzles = true;
let score = 0;

score = 10;

console.log(displayName);
console.log(birthYear);
console.log(likesPuzzles);
console.log(score);
```

An equally valid solution could print the score before and after the update. The requirement only says to create, update, and print these values.

## Debugging task solution

```typescript
const city = "Cebu";

let visitCount = 1;
visitCount = 2;

const isSunny = true;

console.log(city);
console.log(visitCount);
console.log(typeof isSunny);
```

The city reassignment was removed because the requirement says the city does not change. `visitCount` stays a number when it is updated. `isSunny` contains the boolean `true`, so `typeof isSunny` prints `boolean`.
