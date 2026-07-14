# Module 16: Same-Origin Policy, CORS, CSP, and Trusted Content

## What you will learn

Separate browser read restrictions, server permission headers, and content-injection defenses.

## Contracts to understand

- Scheme, host, and port.
- A server can allow selected cross-origin browser reads; it is not authentication.
- The responding server.
- The impact and likelihood of unauthorized script, style, frame, and resource execution when correctly configured.
- Untrusted text is displayed without HTML parsing.

## Complete TypeScript example

```ts
const status = document.querySelector("#status");
if (!(status instanceof HTMLElement)) throw new Error("Missing status");

function showMessage(message: string): void {
  status.textContent = message;
}

showMessage(new URL(location.href).searchParams.get("message") ?? "Ready");
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 17](../module-17-files-blobs-object-urls-and-downloads/README.md).

