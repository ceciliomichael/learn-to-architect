# Module 06: Metadata, Social Images, and Document Information

## What you will learn

Metadata describes pages to browsers and sharing services. Use a static metadata export for fixed values and generateMetadata for values that depend on route data.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import type { Metadata } from "next";
export const metadata: Metadata = {
  title: "About | Example",
  description: "Learn about the Example team."
};
```

## Common mistake

Do not update the document title from a client effect when the server can produce correct metadata before the page arrives.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 07](../07-dynamic-segments-search-parameters-and-typed-routes/README.md).