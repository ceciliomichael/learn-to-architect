# Module 13: Component Events and Typed Emits

## What you will learn

A child emits a named event with a typed payload and the parent decides how application state changes.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
const emit = defineEmits<{ save: [name: string] }>();
</script>
<template><button type="button" @click="emit(`save`, `Ada`)">Save Ada</button></template>
```

## Common mistake

Do not reach into the parent or use vague event names and payloads that hide the action.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 14](../14-slots-and-content-composition/README.md).