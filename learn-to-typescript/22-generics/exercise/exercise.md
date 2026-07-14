# Module 22 Exercises

## Exercise 1: Last item

Write `last<T>(values: readonly T[]): T | undefined`. Test strings, numbers, and an empty array.

## Exercise 2: Generic result

Create `Result<T>` with success value `T` and string failure. Write one function returning `Result<string>` and another returning `Result<number>`.

## Exercise 3: Pair different values

Create `Pair<First, Second>` and a generic `makePair` function. Confirm that `makePair("age", 24)` preserves string and number positions.

## Exercise 4: Constrain an identifier

Write `describeId<T extends { id: string }>(value: T): string`. Call it with an object that also has `name` and confirm the original object type remains available outside the function.

## Exercise 5: Remove a pointless generic

Explain why this does not need `T`, then simplify it:

```typescript
function logAnything<T>(value: T): void {
  console.log(value);
}
```

## Completion checklist

- [ ] I preserved an input-output type relationship.
- [ ] I let TypeScript infer useful type arguments.
- [ ] I created a generic alias.
- [ ] I used the smallest useful constraint.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
