# Module 09: State Snapshots, Queued Updates, and Functional Updates

## What you will learn

Each render sees a state snapshot; use functional updates when the next value depends on the queued previous value.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import type { Dispatch, SetStateAction } from "react";
export function incrementTwice(setCount: Dispatch<SetStateAction<number>>) {
  setCount(previous => previous + 1);
  setCount(previous => previous + 1);
}
```

## Common mistake

Do not expect a setter to change the current render variable immediately.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 10](../module-10-updating-objects-and-arrays-immutably/README.md).