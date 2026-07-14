# Module 15: Component v-model and Fallthrough Attributes

## What you will learn

Component v-model is a prop and update event contract, while fallthrough attributes let a wrapper preserve useful HTML attributes and listeners on the intended root element.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
const model = defineModel<string>({ required: true });
</script>
<template><label>Name <input v-model="model" /></label></template>
```

## Common mistake

Do not swallow labels, accessibility attributes, classes, or listeners in a wrapper component.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 16](../module-16-composables-and-reusable-stateful-logic/README.md).