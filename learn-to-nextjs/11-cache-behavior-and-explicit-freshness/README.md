# Module 11: Cache Behavior and Explicit Freshness

## What you will learn

Treat freshness as an explicit product decision. Know whether data can be reused, for how long, and what event makes it stale, then use the current cache and revalidation APIs deliberately.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { cacheLife } from "next/cache";
async function loadCatalog() {
  "use cache";
  cacheLife("minutes");
  return readCatalog();
}
```

## Common mistake

Do not assume every fetch has the same cache behavior or hide stale-data requirements behind framework defaults.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 12](../12-server-functions-server-actions-and-mutations/README.md).