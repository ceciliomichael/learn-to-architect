# Module 12: Async Ownership, Abort Signals, Timeouts, and Stale Results

## What you will learn

Cancel obsolete requests and prevent an older result from replacing newer UI state.

## Contracts to understand

- The view or operation that starts it must define completion, cancellation, errors, and cleanup.
- Its result is obsolete and should not consume resources or overwrite newer intent.
- Cancellation can race with completion, so identity prevents stale commits.
- Not when cancellation was an expected user or lifecycle action.
- A documented policy that aborts or stops waiting, not proof the server stopped work.

## Complete TypeScript example

```ts
let current: AbortController | null = null;

async function search(query: string): Promise<void> {
  current?.abort();
  const controller = new AbortController();
  current = controller;

  try {
    const url = new URL("/api/search", location.origin);
    url.searchParams.set("q", query);
    const response = await fetch(url, { signal: controller.signal });
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const data: unknown = await response.json();

    if (current === controller) console.log(data);
  } catch (error) {
    if (!(error instanceof DOMException && error.name === "AbortError")) {
      throw error;
    }
  }
}
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 13](../module-13-json-boundaries-and-runtime-validation/README.md).

