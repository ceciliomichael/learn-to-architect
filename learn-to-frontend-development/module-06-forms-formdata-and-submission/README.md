# Module 06: Forms, FormData, and Submission

## What you will learn

Read successful named form controls without manually querying every input.

## Contracts to understand

- Successful named controls and their submitted values, including repeated names and files.
- File inputs contribute File objects.
- Use getAll for their shared name.
- Script should enhance accessible native behavior rather than replace it.
- No. Disabled controls are not successful form controls.

## Complete TypeScript example

```ts
const form = document.querySelector<HTMLFormElement>("#registration");
if (form === null) throw new Error("Expected registration form");

form.addEventListener("submit", (event) => {
  event.preventDefault();
  const data = new FormData(form);
  const name = data.get("fullName");
  const topics = data.getAll("topics");

  if (typeof name !== "string") return;
  console.log({ name: name.trim(), topics });
});
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 07](../module-07-native-validation-custom-rules-and-accessible-errors/README.md).

