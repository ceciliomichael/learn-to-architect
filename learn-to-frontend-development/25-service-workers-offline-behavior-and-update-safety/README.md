# Module 25: Service Workers, Offline Behavior, and Update Safety

## What you will learn

Add offline behavior only with explicit cache scope, fallback, version, and update rules.

## Contracts to understand

- Requests within its controlled scope after activation and control.
- Data freshness, mutations, authentication, cache limits, and conflict behavior need product rules.
- It separates deployments and enables removal or migration of stale assets.
- No. Cache policy must inspect request and response suitability.
- An older worker may control existing clients while a new worker waits or activates.

## Complete TypeScript example

```ts
if ("serviceWorker" in navigator) {
  window.addEventListener("load", () => {
    void navigator.serviceWorker.register("/service-worker.js", {
      scope: "/",
    });
  });
}
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 26](../26-build-configure-deploy-and-maintain-a-browser-application/README.md).

