# Module 14: Route Handlers and HTTP Contracts

## What you will learn

A route handler implements an HTTP contract with Web Request and Response APIs. Parse input, validate it, enforce access, choose status codes, and return a stable response shape.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
export async function POST(request: Request) {
  const session = await requireApiSession(request);
  const input = parseCreateItem(await request.json());
  const item = await createItem(session.userId, input);
  return Response.json(item, { status: 201 });
}
```

## Common mistake

Do not make route handlers thin unsafe tunnels to a database or external service.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 15](../15-forms-runtime-validation-and-action-state/README.md).