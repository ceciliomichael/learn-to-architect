# Module 06: Class and Style Bindings

## What you will learn

Class and style bindings can combine fixed presentation with reactive state while keeping the state meaning separate from CSS details.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
import { ref } from "vue";
const active = ref(false);
</script>
<template><button :class="{ active }" :aria-pressed="active" @click="active = !active">Notifications</button></template>
```

## Common mistake

Do not encode application truth only as a color or replace semantic disabled and hidden behavior with styling alone.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 07](../module-07-conditional-and-list-rendering-with-stable-keys/README.md).