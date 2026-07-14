# Module 07: Native Validation, Custom Rules, and Accessible Errors

## What you will learn

Combine built-in constraints with domain validation and a visible, associated correction message.

## Contracts to understand

- It clears the custom error.
- No. The server repeats every trusted rule.
- After validation determines the current value is invalid, according to the interaction policy.
- Users need a perceivable explanation and correction, not only a state flag.
- Preserve their values whenever safe so users correct only the problem.

## Complete TypeScript example

```ts
const email = document.querySelector<HTMLInputElement>("#email");
const error = document.querySelector<HTMLParagraphElement>("#email-error");

if (email === null || error === null) throw new Error("Missing form UI");

email.addEventListener("input", () => {
  const allowed = email.value.endsWith("@example.test");
  email.setCustomValidity(allowed ? "" : "Use your example.test address.");
  email.setAttribute("aria-invalid", String(!allowed));
  error.textContent = allowed ? "" : "Use your example.test address.";
});
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 08](../module-08-ui-state-and-predictable-rendering-without-a-framework/README.md).

