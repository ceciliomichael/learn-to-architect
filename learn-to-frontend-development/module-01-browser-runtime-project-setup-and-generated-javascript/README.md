# Module 01: Browser Runtime, Project Setup, and Generated JavaScript

## What you will learn

Connect a strict TypeScript source file to an HTML entry point and distinguish source, generated JavaScript, and browser execution.

## Contracts to understand

- Browsers execute JavaScript; a compiler or development tool removes TypeScript-only syntax first.
- The authored HTML, CSS, TypeScript, configuration, manifest, and reviewed lock file, not generated dependency folders.
- It exposes missing null checks and unsafe assumptions before browser execution.
- Generated JavaScript locations back to the authored source for debugging.
- Browser modules, URL resolution, and security policies behave more like deployment over HTTP than direct file loading.

## Complete TypeScript example

```ts
const message: string = "Browser TypeScript is running.";
const output = document.querySelector<HTMLParagraphElement>("#output");

if (output === null) {
  throw new Error("Expected #output");
}

output.textContent = message;
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 02](../module-02-the-dom-tree-and-safe-element-queries/README.md).

