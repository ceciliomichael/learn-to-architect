# Module 22: Component Testing and Accessible Queries

## What you will learn

Component tests should query by accessible role, name, label, and visible behavior.

## Install the testing dependencies

Run this inside `react-course`:

```text
npm install --save-dev vitest jsdom @testing-library/react @testing-library/user-event @testing-library/jest-dom
npm pkg set scripts.test="vitest run"
npm pkg set scripts.test:watch="vitest"
```

Create `vitest.config.ts` with a `jsdom` test environment and a setup file that imports `@testing-library/jest-dom/vitest`. These packages are development tools, so they do not belong in the production dependency list.

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

Continue to [Module 23](../23-rendering-performance-profiling-and-measured-optimization/README.md).
