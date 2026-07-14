# Module 04: Server and Client Component Boundaries

## What you will learn

Components in the App Router are Server Components unless a client boundary is declared. Add use client only where browser state, effects, event handlers, or browser APIs are required.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
// app/counter.tsx
"use client";
import { useState } from "react";
export function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(value => value + 1)}>Count: {count}</button>;
}
```

## Common mistake

Do not place use client on a whole route tree just because one small button is interactive.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 05](../module-05-css-images-fonts-and-static-assets/README.md).