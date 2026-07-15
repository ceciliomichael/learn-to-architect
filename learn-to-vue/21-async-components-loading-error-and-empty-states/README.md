# Module 21: Async Components, Loading, Error, and Empty States

## What you will learn

Async components can delay code loading, while data work needs explicit loading, empty, error, success, cancellation, and retry behavior.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
import { defineAsyncComponent } from "vue";
const ReportPanel = defineAsyncComponent({ loader: () => import("./ReportPanel.vue"), loadingComponent: () => import("./LoadingPanel.vue"), errorComponent: () => import("./ErrorPanel.vue") });
</script>
<template><ReportPanel /></template>
```

## Common mistake

Do not confuse a component download fallback with the data-loading state inside that component.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 22](../22-component-and-end-to-end-testing/README.md).