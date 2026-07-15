# Module 17: Authentication and Session Lifetimes

## What you will learn

Authentication proves which session is making a request, and session design must define creation, rotation, expiry, revocation, and secure cookie behavior.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { cookies } from "next/headers";
export async function requireSession() {
  const token = (await cookies()).get("session")?.value;
  const session = token ? await findValidSession(token) : null;
  if (session === null) throw new Error("Authentication required");
  return session;
}
```

## Common mistake

Do not invent password or session cryptography when a maintained authentication solution fits the application.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 18](../18-authorization-in-pages-actions-and-route-handlers/README.md).