# Module 23: Accessibility, Security Headers, and Untrusted Content

## What you will learn

Preserve semantic HTML and keyboard behavior, apply security headers deliberately, validate untrusted content, and avoid rendering raw HTML unless it has a proven sanitization boundary.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
export function SafeComment({ text }: { text: string }) {
  return <p className="comment">{text}</p>;
}
```

## Common mistake

Do not consider TypeScript, React escaping, or a Content Security Policy a replacement for input validation and authorization.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 24](../module-24-performance-bundle-boundaries-and-observability/README.md).