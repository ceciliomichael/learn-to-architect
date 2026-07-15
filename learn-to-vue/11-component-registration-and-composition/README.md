# Module 11: Component Registration and Composition

## What you will learn

Import and compose small components so each component owns one understandable part of the interface and communicates through explicit inputs and outputs.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
import PageTitle from "./PageTitle.vue";
</script>
<template><main><PageTitle /><p>Choose a lesson.</p></main></template>
```

## Common mistake

Do not create one giant page component or rely on hidden global registration.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 12](../12-props-runtime-declarations-and-one-way-data-flow/README.md).