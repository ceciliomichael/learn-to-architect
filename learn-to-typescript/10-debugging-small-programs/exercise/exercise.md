# Module 10 Exercises

For every task, write the expected result before changing the code.

## Warm-up: Classify the problem

Classify each example as primarily a syntax, type, runtime, or logic problem.

```typescript
console.log("Start";
```

```typescript
let total = 0;
total = "none";
```

```typescript
const names = ["Rae"];
console.log(names[4].toUpperCase());
```

```typescript
const price = 50;
const quantity = 3;
console.log(price + quantity);
```

Assume the last example is meant to calculate a purchase total.

## Guided debugging: Incorrect average

The expected average is `20`, but the program prints `30`:

```typescript
const values = [10, 20, 30];
let total = 0;

for (const value of values) {
  total = value;
}

const average = total / values.length;
console.log(average);
```

1. Add a trace before and after the update.
2. Explain what the trace reveals.
3. Make the smallest correction.
4. Remove the trace.
5. Test with `[5, 5]` as well.

## Independent debugging: Find a task

Fix the function so it returns the title of the first incomplete task, or `"All tasks complete"` when none exists.

```typescript
function findNextTask(tasks: { title: string; isComplete: boolean }[]) {
  const task = tasks.find((item) => item.isComplete);
  return task.title;
}
```

Test with:

```typescript
const mixedTasks = [
  { title: "Read", isComplete: true },
  { title: "Practice", isComplete: false },
];

const completeTasks = [
  { title: "Read", isComplete: true },
];
```

## Boundary task: Delivery fee

The rule is:

- orders of `500` or more have free delivery
- smaller orders have a `50` delivery fee

This function is wrong at one boundary:

```typescript
function calculateDeliveryFee(orderTotal: number) {
  if (orderTotal > 500) {
    return 0;
  }

  return 50;
}
```

Test `499`, `500`, and `501`. Correct the condition.

## Completion checklist

- [ ] I wrote expected and actual behavior.
- [ ] I classified the kind of problem.
- [ ] I traced a changing value.
- [ ] I tested an empty or missing case.
- [ ] I tested exact boundaries.

Then compare with the [exercise solutions](../answers/exercise/exercise-solutions.md).
