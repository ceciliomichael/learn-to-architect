# Module 10: Updating Objects and Arrays Immutably

## What you will learn

Replace state objects and arrays without mutation so React and readers can observe a new value.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
type Item = { id: string; label: string };
export function addItem(items: Item[], label: string): Item[] {
  return [...items, { id: crypto.randomUUID(), label }];
}
```

## Common mistake

Do not push into a state array or edit a nested state object in place.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 11](../11-controlled-and-uncontrolled-form-inputs/README.md).