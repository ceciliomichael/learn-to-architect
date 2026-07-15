# Module 24: Build, Configure, Deploy, and Maintain a React Application

## What you will learn

Build and test the exact production artifact, expose only public configuration, and verify asset paths and rollback behavior.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
function parsePublicUrl(value: unknown): URL {
  if (typeof value !== "string") throw new Error("Missing public API URL");
  const url = new URL(value);
  if (url.protocol !== "https:") throw new Error("Public API URL must use HTTPS");
  return url;
}
export const apiBase = parsePublicUrl(import.meta.env.VITE_PUBLIC_API_BASE);
```

## Common mistake

Do not embed secrets in client bundles or release an untested development build.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Next.js](../../learn-to-nextjs/README.md).