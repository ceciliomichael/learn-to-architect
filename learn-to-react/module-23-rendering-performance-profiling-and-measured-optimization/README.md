# Module 23: Rendering Performance, Profiling, and Measured Optimization

## What you will learn

Profile first, keep state local, and optimize measured rendering work rather than adding memoization everywhere.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { useMemo } from "react";
type Item = { id: string; label: string };
export function useVisibleItems(items: Item[], query: string) {
  return useMemo(() => items.filter(item => item.label.includes(query)), [items, query]);
}
```

## Common mistake

Do not use memo, useMemo, or useCallback without a demonstrated reason.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 24](../module-24-build-configure-deploy-and-maintain-a-react-application/README.md).