# Module 10: Server Data Fetching and Request Ownership

## What you will learn

Fetch data in the server component or server function that owns its use, validate the response, and keep credentials on the server.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
type Product = { id: string; name: string };
async function loadProducts(): Promise<Product[]> {
  const response = await fetch("https://example.test/products");
  if (!response.ok) throw new Error("Products could not be loaded");
  return validateProducts(await response.json());
}
```

## Common mistake

Do not fetch server-owned data through an unnecessary client effect and extra internal HTTP hop.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 11](../module-11-cache-behavior-and-explicit-freshness/README.md).