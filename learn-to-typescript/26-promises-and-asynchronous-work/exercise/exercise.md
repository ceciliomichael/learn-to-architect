# Module 26 Exercises

## Exercise 1: Predict order

Predict and verify the output:

```typescript
console.log("A");
Promise.resolve("B").then((value) => console.log(value));
console.log("C");
```

## Exercise 2: Delay a value

Write `delayValue<T>(value: T, milliseconds: number): Promise<T>`. Resolve with the original value after a timer. Test it with a string and a number.

## Exercise 3: Transform a chain

Start with `Promise.resolve(5)`. Use two `then` calls to double it and then create `"Result: 10"`. Print the final value and record each Promise type.

## Exercise 4: Handle rejection

Write a function returning `Promise<number>` that rejects with an Error for a negative input. Handle both success and failure and narrow the error.

## Exercise 5: Find a missing return

Fix the chain so the final result is `6`:

```typescript
Promise.resolve(3)
  .then((value) => {
    value * 2;
  })
  .then((value) => console.log(value));
```

## Completion checklist

- [ ] I distinguished a Promise from its value.
- [ ] I predicted synchronous and delayed output order.
- [ ] I returned transformations from handlers.
- [ ] I narrowed a rejection value.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
