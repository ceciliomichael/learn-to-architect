# Module 22: Error States, Logging, and User Recovery

## What you will learn

Show an actionable user state while recording technical evidence without exposing sensitive data.

## Contracts to understand

- What failed in user terms and what safe recovery is available.
- Useful context and correlation identifiers without secrets or unnecessary personal data.
- Retries need limits, cancellation, duplicate-action protection, and a clear triggering user.
- No. Expected empty, validation, offline, unauthorized, and server failures need distinct actions.
- Recoverable failure should not force users to repeat valid work.

## Complete TypeScript example

```ts
function showLoadFailure(container: HTMLElement, retry: () => void): void {
  const message = document.createElement("p");
  message.textContent = "Products could not be loaded.";

  const button = document.createElement("button");
  button.type = "button";
  button.textContent = "Try again";
  button.addEventListener("click", retry, { once: true });

  container.replaceChildren(message, button);
}
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 23](../module-23-rendering-network-and-asset-performance/README.md).

