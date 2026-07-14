# Module 02: Single-File Components and script setup

## What you will learn

A Single-File Component keeps one component template, logic, and scoped presentation together. script setup exposes its top-level bindings directly to that component template.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
const title = "Welcome";
</script>

<template>
  <h1>{{ title }}</h1>
</template>
```

## Common mistake

Do not place unrelated application services in a component file or assume scoped styles can never affect child component roots.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 03](../module-03-template-syntax-and-safe-expressions/README.md).