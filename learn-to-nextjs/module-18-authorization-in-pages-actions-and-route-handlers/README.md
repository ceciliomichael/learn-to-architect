# Module 18: Authorization in Pages, Actions, and Route Handlers

## What you will learn

Authorization decides whether the authenticated identity may perform this exact operation on this exact resource. Enforce it beside every protected read and write.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
export async function deleteProject(projectId: string, userId: string) {
  const project = await findProject(projectId);
  if (project === null || project.ownerId !== userId) throw new Error("Not allowed");
  await removeProject(projectId);
}
```

## Common mistake

Do not protect only navigation or page rendering while leaving actions and route handlers callable.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 19](../module-19-databases-transactions-and-connection-boundaries/README.md).