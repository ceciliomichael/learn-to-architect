# Module 03: Pages, Layouts, Links, and Navigation

## What you will learn

A page supplies a route, a layout wraps descendant routes, and Link performs accessible client navigation while retaining normal link behavior.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import Link from "next/link";
export default function RootLayout({ children }: Readonly<{ children: React.ReactNode }>) {
  return <html lang="en"><body><nav><Link href="/">Home</Link></nav>{children}</body></html>;
}
```

## Common mistake

Do not use click handlers or window.location for ordinary navigation that should be a link.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 04](../module-04-server-and-client-component-boundaries/README.md).