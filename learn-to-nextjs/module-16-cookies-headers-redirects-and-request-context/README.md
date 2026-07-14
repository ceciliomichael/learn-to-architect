# Module 16: Cookies, Headers, Redirects, and Request Context

## What you will learn

Cookies and headers belong to the current request context, redirects end the current response path, and reading request-specific values can affect rendering and caching behavior.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { cookies } from "next/headers";
export async function readTheme() {
  const store = await cookies();
  return store.get("theme")?.value === "dark" ? "dark" : "light";
}
```

## Common mistake

Do not treat cookies as general client state or continue code after a redirect as if a normal value was returned.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 17](../module-17-authentication-and-session-lifetimes/README.md).