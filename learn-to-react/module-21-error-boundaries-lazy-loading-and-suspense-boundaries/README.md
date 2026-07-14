# Module 21: Error Boundaries, Lazy Loading, and Suspense Boundaries

## What you will learn

Error boundaries contain rendering failures, lazy loading splits code, and Suspense boundaries represent supported waiting work.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { lazy, Suspense } from "react";
const Settings = lazy(() => import("./Settings"));
export function SettingsPage() {
  return <Suspense fallback={<p role="status">Loading settings...</p>}><Settings /></Suspense>;
}
```

## Common mistake

Do not expect an error boundary to catch every event-handler or server failure.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 22](../module-22-component-testing-and-accessible-queries/README.md).