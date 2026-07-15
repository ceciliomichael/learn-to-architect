# Module 17: Files, Blobs, Object URLs, and Downloads

## What you will learn

Read user-selected files within limits and release temporary object URLs.

## Contracts to understand

- No. They are hints and metadata; trusted processing validates actual content.
- To bound memory, processing time, and user mistakes.
- A temporary origin-scoped URL referring to a Blob or File.
- To release the browser-held reference when no longer needed.
- No. Upload requires an explicit request.

## Complete TypeScript example

```ts
const input = document.querySelector<HTMLInputElement>("#photo");
const preview = document.querySelector<HTMLImageElement>("#preview");
if (input === null || preview === null) throw new Error("Missing file UI");

let currentUrl: string | null = null;
input.addEventListener("change", () => {
  const file = input.files?.[0];
  if (file === undefined || !file.type.startsWith("image/") || file.size > 2_000_000) return;

  if (currentUrl !== null) URL.revokeObjectURL(currentUrl);
  currentUrl = URL.createObjectURL(file);
  preview.src = currentUrl;
});
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 18](../18-timers-animation-frames-and-observer-apis/README.md).

