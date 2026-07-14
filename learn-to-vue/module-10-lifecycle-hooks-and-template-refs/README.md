# Module 10: Lifecycle Hooks and Template Refs

## What you will learn

Lifecycle hooks schedule work around component mounting and removal, while template refs provide limited DOM access after mounting. Clean up every owned external resource.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
import { onMounted, onUnmounted, useTemplateRef } from "vue";
const field = useTemplateRef<HTMLInputElement>("field");
let timer = 0;
onMounted(() => { field.value?.focus(); timer = window.setInterval(() => {}, 1000); });
onUnmounted(() => window.clearInterval(timer));
</script>
<template><input ref="field" aria-label="Search" /></template>
```

## Common mistake

Do not read a template ref before mount or leave timers, observers, and subscriptions active after unmount.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 11](../module-11-component-registration-and-composition/README.md).