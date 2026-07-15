# Module 16: Composables and Reusable Stateful Logic

## What you will learn

A composable is a function that uses Vue reactivity to reuse stateful behavior. Each call owns its state unless a shared owner is intentionally defined.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```ts
import { onUnmounted, ref } from "vue";
export function useClock() {
  const now = ref(new Date());
  const timer = window.setInterval(() => { now.value = new Date(); }, 1000);
  onUnmounted(() => window.clearInterval(timer));
  return { now };
}
```

## Common mistake

Do not treat every helper as a composable or perform hidden global work merely because a function name begins with use.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 17](../17-watchers-watcheffect-and-external-synchronization/README.md).