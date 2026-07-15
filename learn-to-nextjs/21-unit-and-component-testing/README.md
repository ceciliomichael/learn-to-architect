# Module 21: Unit and Component Testing

## What you will learn

Unit tests cover isolated rules and component tests cover rendered behavior at the smallest useful boundary. Mock only the external boundary the test does not own.

## Install the component-test tools

```text
npm install --save-dev vitest jsdom @vitejs/plugin-react @testing-library/react @testing-library/jest-dom
npm pkg set scripts.test="vitest run"
npm pkg set scripts.test:watch="vitest"
```

Create a Vitest configuration using the React plugin, a `jsdom` environment, and a setup file importing `@testing-library/jest-dom/vitest`. Keep server-only rule tests in the Node environment and DOM component tests in `jsdom`.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { render, screen } from "@testing-library/react";
import PageTitle from "./page-title";
test("shows the supplied title", () => {
  render(<PageTitle title="Projects" />);
  expect(screen.getByRole("heading", { name: "Projects" })).toBeVisible();
});
```

## Common mistake

Do not test framework internals or replace all server behavior with mocks that can never detect integration mistakes.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 22](../22-end-to-end-testing-and-production-like-data/README.md).
