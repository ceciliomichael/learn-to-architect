# Module 14: Slots and Content Composition

## What you will learn

Slots let a parent supply content while the child owns surrounding structure, and named or scoped slots make those responsibilities explicit.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<template><section><header><slot name="title" /></header><div><slot /></div></section></template>
```

## Common mistake

Do not replace a simple prop with a slot or let slot content depend on private child details without a scoped-slot contract.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 15](../module-15-component-v-model-and-fallthrough-attributes/README.md).