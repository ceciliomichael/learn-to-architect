# Module 14: Reducers for Related State Transitions

## What you will learn

A reducer names related state transitions and keeps each action deterministic.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
type Action = { type: "increment" } | { type: "reset" };
function reducer(state: number, action: Action) {
  return action.type === "reset" ? 0 : state + 1;
}
```

## Common mistake

Do not use a reducer to hide side effects or accept unvalidated arbitrary actions.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 15](../15-context-and-reducer-composition/README.md).