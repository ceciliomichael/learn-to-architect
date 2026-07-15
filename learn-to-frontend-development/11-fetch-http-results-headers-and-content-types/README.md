# Module 11: Fetch, HTTP Results, Headers, and Content Types

## What you will learn

Treat network completion, HTTP status, content type, and body decoding as separate checks.

## Contracts to understand

- No. It normally resolves with a Response; code checks status.
- The status is in the 200 through 299 range.
- Status alone does not prove the body representation matches the expected decoder.
- unknown.
- Untrusted text must not accidentally change URL path structure.

## Complete TypeScript example

```ts
type Product = { readonly name: string };

async function loadProduct(id: string): Promise<unknown> {
  const url = new URL(`/api/products/${encodeURIComponent(id)}`, location.origin);
  const response = await fetch(url, {
    headers: { Accept: "application/json" },
  });

  if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
  }

  const type = response.headers.get("content-type") ?? "";
  if (!type.includes("application/json")) {
    throw new Error("Expected JSON response");
  }

  return response.json();
}
```

Type-check with strict settings that include the DOM library, run through the course browser project, and inspect both browser output and developer-tool diagnostics.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 12](../12-async-ownership-abort-signals-timeouts-and-stale-results/README.md).

