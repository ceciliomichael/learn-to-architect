# Module 23: Accessibility, Security, and Measured Performance

## What you will learn

Preserve semantic HTML and focus, treat runtime content as untrusted, avoid raw HTML, measure rendering before optimizing, and keep reactive work close to its owner.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
defineProps<{ message: string }>();
</script>
<template><p role="status">{{ message }}</p></template>
```

## Common mistake

Do not claim security from TypeScript or optimize with shallow tricks before profiling the actual problem.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 24](../module-24-build-configure-deploy-and-choose-an-ssr-boundary/README.md).