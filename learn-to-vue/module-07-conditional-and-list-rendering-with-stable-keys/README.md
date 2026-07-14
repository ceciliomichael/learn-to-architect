# Module 07: Conditional and List Rendering with Stable Keys

## What you will learn

Use v-if when content should exist conditionally, v-show for frequent visibility changes, and v-for with a stable key derived from item identity.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
const tasks = [{ id: "read", label: "Read lesson" }];
</script>
<template><p v-if="tasks.length === 0">No tasks.</p><ul v-else><li v-for="task in tasks" :key="task.id">{{ task.label }}</li></ul></template>
```

## Common mistake

Do not combine filtering and list rendering on the same element or use an index key for reorderable data.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 08](../module-08-events-modifiers-and-handler-types/README.md).