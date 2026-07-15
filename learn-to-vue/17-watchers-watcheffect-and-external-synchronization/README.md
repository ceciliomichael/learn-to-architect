# Module 17: Watchers, watchEffect, and External Synchronization

## What you will learn

Use watch for a chosen reactive source and watchEffect for automatically tracked synchronization. Invalidate or clean up stale asynchronous work whenever dependencies change.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```ts
import { ref, watch } from "vue";
const query = ref("");
watch(query, async (value, _oldValue, onCleanup) => {
  const controller = new AbortController();
  onCleanup(() => controller.abort());
  results.value = await search(value, controller.signal);
});
```

## Common mistake

Do not use watchers for values that computed can derive or allow an older request to overwrite a newer result.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 18](../18-provide-inject-and-dependency-boundaries/README.md).