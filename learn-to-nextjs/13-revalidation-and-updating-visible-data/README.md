# Module 13: Revalidation and Updating Visible Data

## What you will learn

After a successful mutation, update or invalidate the cached view that represents the changed data so the next render tells the truth.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { revalidatePath } from "next/cache";
export async function saveItem(input: ItemInput) {
  await database.transaction(() => insertItem(input));
  revalidatePath("/items");
}
```

## Common mistake

Do not revalidate before the database change commits or clear unrelated cached data without a reason.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 14](../14-route-handlers-and-http-contracts/README.md).