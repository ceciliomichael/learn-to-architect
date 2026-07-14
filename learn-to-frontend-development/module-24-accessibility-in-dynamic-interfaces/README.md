# Module 24: Accessibility in Dynamic Interfaces

## What you will learn

Preserve names, focus, status announcements, and keyboard behavior as the DOM changes.

## Contracts to understand

- It announces relevant updates when assistive technology is ready without abruptly interrupting.
- No. Announce meaningful status not already conveyed through focus or controls.
- To a logical surviving control according to the interaction design.
- They preserve expected keyboard and accessibility behavior during updates.
- Duplicate actions while still communicating progress and recovery.

## Complete TypeScript example

```ts
const status = document.querySelector<HTMLParagraphElement>("#save-status");
const save = document.querySelector<HTMLButtonElement>("#save");
if (status === null || save === null) throw new Error("Missing save UI");

save.addEventListener("click", async () => {
  save.disabled = true;
  status.textContent = "Saving";
  try {
    await Promise.resolve();
    status.textContent = "Saved";
  } finally {
    save.disabled = false;
  }
});
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 25](../module-25-service-workers-offline-behavior-and-update-safety/README.md).

