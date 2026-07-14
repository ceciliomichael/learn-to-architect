# Module 10 Exercise Solutions

## Warm-up classifications

1. `console.log("Start";` has a syntax problem because the call is missing a closing parenthesis.
2. Assigning `"none"` to a number variable is a type problem.
3. Calling a method on a missing array item is a runtime problem in the shown compiler conditions. The missing index produces `undefined`, which has no `toUpperCase` method.
4. Adding price and quantity is a logic problem when the intention is a purchase total. Both values are valid numbers, so the type checker does not know the formula should multiply.

## Guided debugging solution

A useful trace is:

```typescript
const values = [10, 20, 30];
let total = 0;

for (const value of values) {
  console.log(`Before: total=${total}, value=${value}`);
  total = value;
  console.log(`After: total=${total}`);
}
```

It shows that `total` is replaced by each item. The corrected program is:

```typescript
const values = [10, 20, 30];
let total = 0;

for (const value of values) {
  total = total + value;
}

const average = total / values.length;
console.log(average);
```

For `[10, 20, 30]`, the result is `20`. For `[5, 5]`, it is `5`.

One more boundary remains: an empty array would divide zero by zero and produce `NaN`. The given task did not require empty input, but noticing it is good debugging work.

## Independent debugging solution

```typescript
function findNextTask(tasks: { title: string; isComplete: boolean }[]) {
  const task = tasks.find((item) => !item.isComplete);

  if (task === undefined) {
    return "All tasks complete";
  }

  return task.title;
}

const mixedTasks = [
  { title: "Read", isComplete: true },
  { title: "Practice", isComplete: false },
];

const completeTasks = [
  { title: "Read", isComplete: true },
];

console.log(findNextTask(mixedTasks));
console.log(findNextTask(completeTasks));
```

Expected output:

```text
Practice
All tasks complete
```

The callback needed to match incomplete items. The function also needed a path for the `undefined` result from `find`.

## Boundary task solution

```typescript
function calculateDeliveryFee(orderTotal: number) {
  if (orderTotal >= 500) {
    return 0;
  }

  return 50;
}

console.log(calculateDeliveryFee(499));
console.log(calculateDeliveryFee(500));
console.log(calculateDeliveryFee(501));
```

Expected output:

```text
50
0
0
```

The phrase `500 or more` requires `>=`, not `>`.
