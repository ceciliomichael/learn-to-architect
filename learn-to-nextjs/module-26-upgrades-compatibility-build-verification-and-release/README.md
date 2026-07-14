# Module 26: Upgrades, Compatibility, Build Verification, and Release

## What you will learn

Upgrade dependencies intentionally, read official migration notes, verify supported runtimes, and run linting, type checks, tests, and a production build before release.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
// package.json scripts used by the release check
const releaseCommands = ["npm run lint", "npm run typecheck", "npm test", "npm run build"] as const;
```

## Common mistake

Do not combine an unreviewed framework upgrade with unrelated feature changes or release only from a development server.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Return to the [Web Development Learning Path](../../learning-paths/web-development.md) to choose another specialization.