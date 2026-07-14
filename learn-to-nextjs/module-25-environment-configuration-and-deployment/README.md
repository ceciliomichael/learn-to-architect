# Module 25: Environment Configuration and Deployment

## What you will learn

Validate environment variables on the server, expose only explicitly public values, build in the deployment target, and document migrations, health checks, and rollback.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { z } from "zod";
const Environment = z.object({ DATABASE_URL: z.string().url(), SESSION_SECRET: z.string().min(32) });
export const environment = Environment.parse(process.env);
```

## Common mistake

Do not place secrets in NEXT_PUBLIC variables or assume a successful local development run proves deployability.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 26](../module-26-upgrades-compatibility-build-verification-and-release/README.md).