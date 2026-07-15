# Module 19: Vue Router and Navigation

## What you will learn

Vue Router maps URLs to views, preserves real links, parses route values as untrusted input, and supports nested layouts and navigation guards.

## Install and register Vue Router

The course did not generate Router in Module 01. Add it now:

```text
npm install vue-router
```

After creating `src/router.ts`, import the router in `src/main.ts` and register it before mounting:

```ts
createApp(App).use(router).mount(root);
```

Installation records the runtime dependency in `package.json` and the exact resolution in `package-lock.json`.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```ts
import { createRouter, createWebHistory } from "vue-router";
export const router = createRouter({
  history: createWebHistory(),
  routes: [{ path: "/", component: () => import("./views/HomeView.vue") }]
});
```

## Common mistake

Do not replace links with clickable containers or put authorization only in a client navigation guard.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 20](../20-pinia-and-shared-application-state/README.md).
