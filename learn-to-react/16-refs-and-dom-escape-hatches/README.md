# Module 16: Refs and DOM Escape Hatches

## What you will learn

Refs hold values that do not drive rendering and provide deliberate access to DOM escape hatches.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { useRef } from "react";
export function SearchField() {
  const inputRef = useRef<HTMLInputElement>(null);
  return <><input ref={inputRef} aria-label="Search" /><button type="button" onClick={() => inputRef.current?.focus()}>Focus search</button></>;
}
```

## Common mistake

Do not read or write refs during rendering or replace declarative UI with manual DOM mutation.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 17](../17-effects-for-external-synchronization/README.md).