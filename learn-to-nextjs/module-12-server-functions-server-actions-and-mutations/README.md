# Module 12: Server Functions, Server Actions, and Mutations

## What you will learn

A server function runs trusted server code, and a server action can be invoked as a mutation endpoint from the UI. Validate input and authenticate and authorize every call.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
"use server";
export async function renameProject(formData: FormData) {
  const session = await requireSession();
  const name = parseProjectName(formData.get("name"));
  await updateOwnedProject(session.userId, name);
}
```

## Common mistake

Do not trust an action merely because its calling button was rendered by your application.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 13](../module-13-revalidation-and-updating-visible-data/README.md).