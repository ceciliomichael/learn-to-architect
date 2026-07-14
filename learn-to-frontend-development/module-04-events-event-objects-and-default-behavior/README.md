# Module 04: Events, Event Objects, and Default Behavior

## What you will learn

Respond to native events, read the correct event target, and cancel default behavior only after replacing it.

## Contracts to understand

- Submit covers keyboard submission and other native form submission paths.
- The element whose listener is currently running.
- The deepest dispatched target, which may be a descendant.
- When code intentionally replaces a cancelable native behavior.
- No. Cancellation and propagation are separate.

## Complete TypeScript example

```ts
const form = document.querySelector<HTMLFormElement>("#search-form");
if (form === null) throw new Error("Expected search form");

form.addEventListener("submit", (event) => {
  event.preventDefault();
  const data = new FormData(form);
  const query = data.get("query");

  if (typeof query === "string") {
    console.log(query.trim());
  }
});
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 05](../module-05-propagation-delegation-and-listener-cleanup/README.md).

