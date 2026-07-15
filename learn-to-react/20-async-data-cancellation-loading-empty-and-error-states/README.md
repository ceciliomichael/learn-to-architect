# Module 20: Async Data, Cancellation, Loading, Empty, and Error States

## What you will learn

Async UI needs owned cancellation plus distinct loading, empty, error, and success states, and stale results must not overwrite newer intent.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
type LoadState<T> = { status: "loading" } | { status: "error"; message: string } | { status: "ready"; data: T };
```

## Common mistake

Do not start an unowned fetch in an effect without cleanup and race handling.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 21](../21-error-boundaries-lazy-loading-and-suspense-boundaries/README.md).