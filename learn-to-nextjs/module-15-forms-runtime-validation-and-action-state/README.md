# Module 15: Forms, Runtime Validation, and Action State

## What you will learn

Forms should work with browser semantics first, validate on the server, preserve entered values when useful, and expose pending and field errors through accessible action state.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
"use client";
import { useActionState } from "react";
export function NameForm({ action }: { action: (state: FormState, data: FormData) => Promise<FormState> }) {
  const [state, formAction, pending] = useActionState(action, { error: "" });
  return <form action={formAction}><label>Name <input name="name" required /></label><p role="alert">{state.error}</p><button disabled={pending}>{pending ? "Saving..." : "Save"}</button></form>;
}
```

## Common mistake

Do not rely only on client validation or disable a form without explaining that submission is in progress.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 16](../module-16-cookies-headers-redirects-and-request-context/README.md).