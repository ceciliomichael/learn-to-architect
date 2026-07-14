# Module 01: Create a Next.js Application and Read the Generated Project

## What you will learn

Create a current App Router project with the official project generator, then read its scripts, dependency versions, TypeScript settings, and app entry files before changing them.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
export default function HomePage() {
  return <main><h1>My first Next.js page</h1></main>;
}
```

## Common mistake

Do not treat generated files as magic or follow older Pages Router tutorials without noticing the difference.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 02](../module-02-app-router-folders-files-and-colocation/README.md).