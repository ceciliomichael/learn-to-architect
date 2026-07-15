# Module 12: Props, Runtime Declarations, and One-Way Data Flow

## What you will learn

Props are one-way readonly inputs. Type declarations help authors, runtime declarations can validate JavaScript callers, and object or array defaults must not be shared mutable instances.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
const props = defineProps<{ title: string; count?: number }>();
</script>
<template><h2>{{ props.title }} ({{ props.count ?? 0 }})</h2></template>
```

## Common mistake

Do not mutate a prop inside a child or copy it into state without a clear editable-draft reason.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 13](../13-component-events-and-typed-emits/README.md).