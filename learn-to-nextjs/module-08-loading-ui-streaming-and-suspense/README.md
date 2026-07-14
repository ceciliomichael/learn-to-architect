# Module 08: Loading UI, Streaming, and Suspense

## What you will learn

A loading file and Suspense boundaries let ready parts render while slower server work continues, but each fallback must be meaningful and accessible.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
export default function Loading() {
  return <p role="status">Loading account details...</p>;
}
```

## Common mistake

Do not add a spinner with no label or create so many boundaries that the page flashes through unrelated placeholders.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 09](../module-09-expected-errors-error-boundaries-and-not-found/README.md).