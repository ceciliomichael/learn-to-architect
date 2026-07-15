# Module 04: Refs, Reactive Objects, and Automatic Unwrapping

## What you will learn

A ref owns one reactive value and a reactive object tracks its properties. Templates unwrap refs for convenient reading, while TypeScript code normally uses value.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
import { reactive, ref } from "vue";
const count = ref(0);
const profile = reactive({ name: "Ada" });
</script>
<template><button @click="count++">{{ profile.name }}: {{ count }}</button></template>
```

## Common mistake

Do not destructure a reactive object carelessly and then expect the separated values to remain reactive.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 05](../05-computed-values-and-derived-state/README.md).