# Module 02: App Router Folders, Files, and Colocation

## What you will learn

Inside app, folders organize route segments while special file names such as page, layout, loading, error, and route give files framework meaning. Ordinary colocated files are not public routes by themselves.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
export default function AccountPage() {
  return <main><h1>Account</h1></main>;
}
// app/account/format-name.ts is colocated code, not a route.
```

## Common mistake

Do not assume every file under app becomes a page or scatter one feature across unrelated folders.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 03](../03-pages-layouts-links-and-navigation/README.md).