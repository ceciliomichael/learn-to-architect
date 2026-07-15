# Module 18: Provide, Inject, and Dependency Boundaries

## What you will learn

Provide and inject pass a dependency through a component subtree. Use typed keys, stable service contracts, and an intentional provider boundary.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```ts
import type { InjectionKey, Ref } from "vue";
export const ThemeKey: InjectionKey<Ref<"light" | "dark">> = Symbol("theme");
```

## Common mistake

Do not use injection as invisible global state or mutate provided state from arbitrary descendants.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 19](../19-vue-router-and-navigation/README.md).