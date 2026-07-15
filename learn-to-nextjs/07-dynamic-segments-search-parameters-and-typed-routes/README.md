# Module 07: Dynamic Segments, Search Parameters, and Typed Routes

## What you will learn

Dynamic segment folders capture path values, search parameters represent query values, and both remain untrusted input even when TypeScript describes their shape.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
type PageProps = { params: Promise<{ productId: string }> };
export default async function ProductPage({ params }: PageProps) {
  const { productId } = await params;
  if (!/^[a-z0-9-]+$/.test(productId)) return <p>Invalid product address.</p>;
  return <h1>Product {productId}</h1>;
}
```

## Common mistake

Do not use route or query values before validating their format and allowed range.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 08](../08-loading-ui-streaming-and-suspense/README.md).