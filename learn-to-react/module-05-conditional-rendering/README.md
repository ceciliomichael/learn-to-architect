# Module 05: Conditional Rendering

## What you will learn

Conditional rendering chooses element output with ordinary JavaScript while preserving meaningful empty and inaccessible states.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
export function Result({ count }: { count: number }) {
  return count === 0 ? <p>No results.</p> : <p>{count} results</p>;
}
```

## Common mistake

Do not hide required content only with a truthy check that mishandles zero or empty text.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 06](../module-06-lists-stable-keys-and-empty-states/README.md).