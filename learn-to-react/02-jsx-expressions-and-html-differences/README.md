# Module 02: JSX, Expressions, and HTML Differences

## What you will learn

JSX describes a React element tree while JavaScript expressions supply values; use className, htmlFor, and camel-cased properties where React differs from HTML source.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
export function Greeting() {
  const name = "Ada";
  return <h1 className="greeting">Hello, {name}</h1>;
}
```

## Common mistake

Do not place statements inside JSX braces or copy HTML attributes without checking React names.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 03](../03-components-imports-exports-and-purity/README.md).