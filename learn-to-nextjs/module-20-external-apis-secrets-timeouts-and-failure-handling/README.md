# Module 20: External APIs, Secrets, Timeouts, and Failure Handling

## What you will learn

Call external APIs only from the environment that may hold their secrets, set a timeout or cancellation policy, validate responses, and translate failures into useful application states.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
const controller = new AbortController();
const timer = setTimeout(() => controller.abort(), 5000);
try {
  const response = await fetch(apiUrl, { signal: controller.signal, headers: { Authorization: `Bearer ${apiToken}` } });
  if (!response.ok) throw new Error(`Upstream failed: ${response.status}`);
  return parseUpstream(await response.json());
} finally {
  clearTimeout(timer);
}
```

## Common mistake

Do not wait forever, log credentials, or assume a successful HTTP status means the response has the expected shape.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 21](../module-21-unit-and-component-testing/README.md).