# Module 03: Template Syntax and Safe Expressions

## What you will learn

Vue templates are HTML-like declarations with directives and JavaScript expressions. Interpolation escapes text, while directives control attributes and behavior.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```vue
<script setup lang="ts">
const learner = { name: "Ada", lessons: 3 };
</script>
<template><p>{{ learner.name }} has {{ learner.lessons }} lessons.</p></template>
```

## Common mistake

Do not put assignments or complex business work in template expressions, and do not render untrusted HTML.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 04](../module-04-refs-reactive-objects-and-automatic-unwrapping/README.md).