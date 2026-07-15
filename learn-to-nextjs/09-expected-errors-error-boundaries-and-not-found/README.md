# Module 09: Expected Errors, Error Boundaries, and Not Found

## What you will learn

Return expected failures as ordinary states, use notFound for missing resources, and use an error boundary for unexpected rendering failures that need containment and recovery.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { notFound } from "next/navigation";
export default async function PostPage({ params }: { params: Promise<{ id: string }> }) {
  const { id } = await params;
  const post = await findPost(id);
  if (post === null) notFound();
  return <article><h1>{post.title}</h1></article>;
}
```

## Common mistake

Do not throw every validation error or expect one root boundary to explain every failure clearly.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 10](../10-server-data-fetching-and-request-ownership/README.md).