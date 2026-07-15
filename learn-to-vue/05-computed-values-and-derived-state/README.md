# Module 05: Computed Values and Derived State

## What you will learn

A computed value derives information from reactive sources and should stay pure, cached by dependency, and free of mutation.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
import { computed, ref } from "vue";
const first = ref("Ada");
const last = ref("Lovelace");
const fullName = computed(() => `${first.value} ${last.value}`);
</script>
<template><p>{{ fullName }}</p></template>
```

## Common mistake

Do not copy calculated data into another ref and synchronize it with a watcher.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 06](../06-class-and-style-bindings/README.md).