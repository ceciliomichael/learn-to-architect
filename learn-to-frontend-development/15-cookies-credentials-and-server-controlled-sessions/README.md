# Module 15: Cookies, Credentials, and Server-Controlled Sessions

## What you will learn

Understand cookie transport while keeping session secrets and authorization on the server.

## Contracts to understand

- Browser JavaScript cannot read them, reducing direct token theft through script injection.
- The cookie is sent only over secure transport, subject to browser rules.
- Whether cookies accompany certain cross-site requests, reducing some CSRF exposure.
- No. The server validates session state and authorization for every protected action.
- Whether cookies and other credentials are included under the selected origin policy.

## Complete TypeScript example

```ts
async function loadAccount(): Promise<unknown> {
  const response = await fetch("/api/account", {
    credentials: "same-origin",
    headers: { Accept: "application/json" },
  });

  if (response.status === 401) return null;
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  return response.json();
}
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 16](../16-same-origin-policy-cors-csp-and-trusted-content/README.md).

