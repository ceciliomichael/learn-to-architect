# Module 13: Choosing Minimal State and Avoiding Contradictions

## What you will learn

Store the minimum complete state and derive everything else during rendering when possible.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
type Item = { id: string; label: string };
export function filterItems(items: Item[], query: string): Item[] {
  const normalized = query.trim().toLowerCase();
  return items.filter(item => item.label.toLowerCase().includes(normalized));
}
```

## Common mistake

Do not store contradictory flags or values that can be calculated from other state.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 14](../module-14-reducers-for-related-state-transitions/README.md).