# Module 01: React Playground, Local Project, and Rendering Root

## What you will learn

Start in an official sandbox or a local strict TypeScript project, identify the DOM root, and render one application tree.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { createRoot } from "react-dom/client";
import { StrictMode } from "react";
import App from "./App";
const root = document.getElementById("root");
if (root === null) throw new Error("Missing #root");
createRoot(root).render(<StrictMode><App /></StrictMode>);
```

## Common mistake

Do not use deprecated Create React App instructions or mount several unrelated roots without a reason.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 02](../module-02-jsx-expressions-and-html-differences/README.md).