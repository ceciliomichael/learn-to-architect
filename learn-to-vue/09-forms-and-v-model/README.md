# Module 09: Forms and v-model

## What you will learn

v-model connects a form control value and its update event, but each control type still follows native HTML semantics and needs a label, validation, and an error path.

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
const name = ref("");
</script>
<template><label>Name <input v-model.trim="name" required /></label><p>Hello, {{ name || "learner" }}.</p></template>
```

## Common mistake

Do not use a placeholder as the only label or assume v-model validates runtime input.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 10](../10-lifecycle-hooks-and-template-refs/README.md).