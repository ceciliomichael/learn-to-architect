# Module 21: DOM Integration and End-to-End Testing

## What you will learn

Test visible behavior through accessible queries, then reserve full browser flows for critical journeys.

## Add the tools at their boundaries

DOM integration tests need a DOM implementation and accessible query helpers:

```text
npm install --save-dev jsdom @testing-library/dom @testing-library/user-event
```

Set the DOM environment at the top of a DOM test with `// @vitest-environment jsdom`.

For real browser flows, initialize Playwright in the existing project:

```text
npm init playwright@latest
```

Choose TypeScript, use `e2e` as the test folder, and install the browser binaries. Run the generated example with `npx playwright test` before replacing it.

## Contracts to understand

- Roles, labels, names, and visible text that users perceive.
- Several units working across a boundary such as form, renderer, and DOM.
- A small set of critical journeys in a real browser and realistic environment.
- They are slow and flaky; wait for a meaningful observable condition.
- DOM, listeners, storage, network handlers, timers, and created data they own.

## Complete TypeScript example

```ts
// Framework-neutral test shape:
document.body.innerHTML = `
  <form id="signup">
    <label for="name">Name</label>
    <input id="name" name="name" required>
    <button>Join</button>
  </form>
`;

const button = document.querySelector("button");
if (!(button instanceof HTMLButtonElement)) throw new Error("Missing button");
button.click();
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 22](../22-error-states-logging-and-user-recovery/README.md).
