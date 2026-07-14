# Module 28 Exercises

## Exercise 1: Save state

Model save state as idle, saving, saved with timestamp, or failed with an error message. Write a render function.

## Exercise 2: Exhaustive switch

Add `assertNever` to the render function. Then add a new `"cancelled"` member and observe the error until you add its case.

## Exercise 3: Result transition

Create events `start`, `succeed`, `fail`, and `reset`. Write a transition function returning the next save state.

## Exercise 4: Repair optional state

Replace this loose shape with a discriminated union:

```typescript
interface FormState {
  submitting: boolean;
  receiptId?: string;
  error?: string;
}
```

## Exercise 5: Boundary explanation

Explain why receiving `{ status: "success" }` from JSON is not safe merely because your local `LoadState` requires data for success.

## Completion checklist

- [ ] Every state has an exact discriminant.
- [ ] Each member contains only its relevant data.
- [ ] I added an exhaustive switch check.
- [ ] I kept runtime validation separate.

Then read the [exercise solutions](../answers/exercise/exercise-solutions.md).
