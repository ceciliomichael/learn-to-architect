# Module 22: Component and End-to-End Testing

## What you will learn

Component tests assert visible behavior through accessible queries, and end-to-end tests exercise critical browser flows against controlled data.

## Install each testing layer

Add component-test dependencies:

```text
npm install --save-dev vitest jsdom @testing-library/vue @testing-library/jest-dom
npm pkg set scripts.test="vitest run"
npm pkg set scripts.test:watch="vitest"
```

Configure Vitest to use `jsdom` and import `@testing-library/jest-dom/vitest` from a setup file. Then initialize real-browser tests:

```text
npm init playwright@latest
```

Choose TypeScript, use `e2e` as the folder, and install the browsers. Component tests and end-to-end tests have different costs and should remain separate scripts.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```ts
import { render, screen } from "@testing-library/vue";
import SaveButton from "./SaveButton.vue";
test("emits save", async () => {
  const view = render(SaveButton);
  await screen.getByRole("button", { name: "Save" }).click();
  expect(view.emitted().save).toHaveLength(1);
});
```

## Common mistake

Do not test private component variables or build an end-to-end suite around arbitrary waits and shared mutable accounts.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 23](../23-accessibility-security-and-measured-performance/README.md).
