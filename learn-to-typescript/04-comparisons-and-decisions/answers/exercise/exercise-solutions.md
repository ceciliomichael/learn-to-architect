# Module 04 Exercise Solutions

## Warm-up solution

```typescript
const currentPages = 40;
const goalPages = 50;

console.log(currentPages >= goalPages);
console.log(currentPages < goalPages);
console.log(currentPages === 40);
```

Expected output:

```text
false
true
true
```

## Guided exercise solution

```typescript
const age = 17;

if (age < 6) {
  console.log("Free ticket");
} else if (age < 18) {
  console.log("Child ticket");
} else if (age < 65) {
  console.log("Standard ticket");
} else {
  console.log("Senior ticket");
}
```

When the program reaches the second condition, it already knows the age is at least 6. This lets each later condition check only the next upper boundary.

## Independent exercise solution

```typescript
const minutesStudied = 35;
const dailyGoal = 45;
const isRestDay = false;
const remainingMinutes = dailyGoal - minutesStudied;

if (isRestDay) {
  console.log("Rest and return tomorrow.");
} else if (minutesStudied >= dailyGoal) {
  console.log("Daily goal complete.");
} else {
  console.log(`${remainingMinutes} minutes remain.`);
}
```

For the given values, the output is:

```text
10 minutes remain.
```

The rest-day check comes first because it changes whether the goal should be considered at all.

## Logic exercise solution

```typescript
const hasLibraryCard = true;
const hasOverdueBook = false;

if (hasLibraryCard && !hasOverdueBook) {
  console.log("Book may be borrowed");
} else {
  console.log("Book may not be borrowed");
}
```

Only `true` for the card and `false` for the overdue book permits borrowing.

## Debugging task solution

```typescript
const score = 92;

if (score >= 90) {
  console.log("Excellent");
} else if (score >= 60) {
  console.log("Pass");
} else {
  console.log("Try again");
}
```

The highest threshold must be checked first. The original first condition accepted `92` immediately, so the second branch could never run for that score. The original second condition also used assignment instead of comparison.
