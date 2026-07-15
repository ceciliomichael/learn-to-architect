# Module 11: Controlled and Uncontrolled Form Inputs

## What you will learn

Controlled inputs receive value and onChange from React state, while uncontrolled inputs keep current value in the DOM; choose deliberately.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { useState } from "react";
export function NameField() {
  const [name, setName] = useState("");
  return <label>Name <input value={name} onChange={event => setName(event.target.value)} /></label>;
}
```

## Common mistake

Do not pass value without an update handler and accidentally freeze an editable control.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 12](../12-lifting-state-and-one-way-data-flow/README.md).