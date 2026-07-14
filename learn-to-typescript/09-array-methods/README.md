# Module 09: Array Methods

## Before you start

Complete Modules 01 to 08. You should understand functions, arrays, objects, loops, and decisions.

## What you will learn

- pass a short function as a callback
- visit items with `forEach`
- transform items with `map`
- keep selected items with `filter`
- search with `find`, `some`, and `every`
- choose a method based on the result you need

## Why this matters

Array methods express common list operations directly. A reader can often understand `filter` or `find` faster than a manual loop with several counters.

## 1. A callback is a function given to another function

Start with a normal function:

```typescript
function printName(name: string) {
  console.log(name);
}

const names = ["Ana", "Bo", "Cy"];
names.forEach(printName);
```

`forEach` calls `printName` once for every item. `printName` is the callback.

For short callbacks, an arrow function keeps the action close to the method call:

```typescript
names.forEach((name) => {
  console.log(name);
});
```

The arrow separates the parameter from the function body. TypeScript knows `name` is a string from the array, so no annotation is needed.

## 2. `forEach` performs an action

```typescript
const prices = [10, 20, 30];

prices.forEach((price) => {
  console.log(`Price: ${price}`);
});
```

Use `forEach` when the goal is an action for each item. It returns `undefined`, not a new array.

A `for...of` loop is still useful when you need `break`, `continue`, or `await` later.

## 3. `map` transforms every item

```typescript
const prices = [10, 20, 30];
const doubledPrices = prices.map((price) => {
  return price * 2;
});

console.log(doubledPrices);
console.log(prices);
```

Expected output:

```text
[20, 40, 60]
[10, 20, 30]
```

`map` returns a new array with one result for each original item. It does not change the original array.

A short callback can return an expression directly:

```typescript
const doubledPrices = prices.map((price) => price * 2);
```

Use the block form while several steps need names or explanation.

## 4. `filter` keeps matching items

```typescript
const scores = [45, 82, 67, 91];
const passingScores = scores.filter((score) => {
  return score >= 60;
});

console.log(passingScores);
```

The callback returns a boolean. Items that produce `true` are included in the new array.

The result may contain fewer items, the same number of items, or no items.

## 5. `find` returns the first match

```typescript
const tasks = [
  { title: "Read", isComplete: true },
  { title: "Practice", isComplete: false },
  { title: "Review", isComplete: false },
];

const firstIncompleteTask = tasks.find((task) => {
  return !task.isComplete;
});
```

`find` returns the first matching item or `undefined` if no item matches.

Check before using it:

```typescript
if (firstIncompleteTask !== undefined) {
  console.log(firstIncompleteTask.title);
}
```

## 6. `some` and `every` answer boolean questions

```typescript
const temperatures = [27, 29, 32];

const hasHotDay = temperatures.some((temperature) => temperature > 30);
const allAreWarm = temperatures.every((temperature) => temperature >= 25);

console.log(hasHotDay);
console.log(allAreWarm);
```

- `some` returns true when at least one item matches.
- `every` returns true when all items match.

For an empty array, `some` returns false and `every` returns true. The second result follows from there being no item that breaks the rule, but it can surprise people. Decide what an empty list should mean in your program.

## 7. Choose by the desired result

| Need | Method |
| --- | --- |
| perform an action for each item | `forEach` |
| produce one new item per old item | `map` |
| keep matching items | `filter` |
| get the first matching item | `find` |
| ask whether at least one item matches | `some` |
| ask whether all items match | `every` |

Methods can be combined, but keep the steps readable:

```typescript
const numbers = [1, 2, 3, 4, 5];
const evenSquares = numbers
  .filter((number) => number % 2 === 0)
  .map((number) => number * number);

console.log(evenSquares);
```

## Predict the result

```typescript
const words = ["sun", "planet", "sky"];
const longWords = words.filter((word) => word.length > 3);
const lengths = longWords.map((word) => word.length);

console.log(longWords);
console.log(lengths);
```

## Common mistakes

### Expecting `forEach` to create an array

Use `map` when you need a transformed array.

### Forgetting `return` in a callback block

Braces require an explicit return when `map`, `filter`, or `find` needs a result.

### Assuming `find` always succeeds

Its result can be `undefined`.

### Using `map` only to print

If you ignore the returned array, `forEach` or a loop better describes the intent.

## Check your understanding

1. What is a callback?
2. Which method returns a new array with the same length?
3. Which method can return `undefined`?
4. What should a `filter` callback return?
5. When might `for...of` be clearer than `forEach`?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 10](../10-debugging-small-programs/README.md) gives you a repeatable method for investigating mistakes.
