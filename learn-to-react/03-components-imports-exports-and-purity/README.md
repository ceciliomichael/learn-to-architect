# Module 03: Components, Imports, Exports, and Purity

## What you will learn

A component is a capitalized function that returns UI and remains pure during rendering; imports and exports define module ownership.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
export default function Status() {
  return <p>Registration is open.</p>;
}
```

## Common mistake

Do not cause network requests, subscriptions, or mutation while rendering.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 04](../04-props-children-and-composition/README.md).