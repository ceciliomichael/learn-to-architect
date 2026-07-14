# Module 18: Timers, Animation Frames, and Observer APIs

## What you will learn

Schedule work with the API matching its timing purpose and clean up when ownership ends.

## Contracts to understand

- No. They are minimum delays affected by task queues, throttling, and page state.
- For visual updates synchronized with a future paint.
- Repeated manual geometry polling for visibility intersections.
- The component or view that created and owns it.
- It delays input, rendering, and other tasks.

## Complete TypeScript example

```ts
const output = document.querySelector("#clock");
if (!(output instanceof HTMLElement)) throw new Error("Missing clock");

const controller = new AbortController();
const timer = window.setInterval(() => {
  output.textContent = new Date().toLocaleTimeString();
}, 1_000);

controller.signal.addEventListener("abort", () => {
  window.clearInterval(timer);
}, { once: true });
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 19](../module-19-custom-elements-shadow-dom-and-web-component-boundaries/README.md).

