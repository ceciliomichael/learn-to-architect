# Module 01: Vue Playground, create-vue, and the Application Root

## What you will learn

Use the official playground for a quick experiment or create-vue for a local strict TypeScript project, then identify the application root and the component mounted into it.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```ts
import { createApp } from "vue";
import App from "./App.vue";
const root = document.querySelector("#app");
if (root === null) throw new Error("Missing #app");
createApp(App).mount(root);
```

## Common mistake

Do not add Vue through unrelated scripts or hide the mount element and entry file before understanding their roles.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 02](../module-02-single-file-components-and-script-setup/README.md).