# Module 22: Component Testing and Accessible Queries

## What you will learn

Component tests should query by accessible role, name, label, and visible behavior.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import { expect, test, vi } from "vitest";
import { SaveButton } from "./SaveButton";
test("calls onSave", async () => {
  const onSave = vi.fn();
  const user = userEvent.setup();
  render(<SaveButton onSave={onSave} />);
  await user.click(screen.getByRole("button", { name: "Save" }));
  expect(onSave).toHaveBeenCalledOnce();
});
```

## Common mistake

Do not test component internals or select elements only through implementation classes.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 23](../module-23-rendering-performance-profiling-and-measured-optimization/README.md).