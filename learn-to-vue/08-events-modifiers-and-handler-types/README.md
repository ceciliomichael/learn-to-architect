# Module 08: Events, Modifiers, and Handler Types

## What you will learn

Event bindings receive browser events or call named handlers, and modifiers express common DOM behavior close to the binding.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
function save(event: MouseEvent) {
  console.log("Saved from", event.currentTarget);
}
</script>
<template><button type="button" @click="save">Save</button></template>
```

## Common mistake

Do not call a handler while rendering or use stop and prevent modifiers without understanding the browser behavior being changed.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 09](../09-forms-and-v-model/README.md).