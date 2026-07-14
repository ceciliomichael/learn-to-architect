# Module 18: Removing Unnecessary Effects

## What you will learn

Remove an effect when derived rendering, an event handler, a key, or an external-store API expresses the behavior directly.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
export function formatFullName(firstName: string, lastName: string): string {
  return `${firstName} ${lastName}`;
}
```

## Common mistake

Do not create effect chains that set state only to trigger another effect.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 19](../module-19-custom-hooks-and-reusable-stateful-behavior/README.md).