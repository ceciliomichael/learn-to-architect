# Module 20: Pinia and Shared Application State

## What you will learn

Pinia stores shared application state and actions when ownership truly spans distant components. Keep local component state local and expose focused store APIs.

## Install and register Pinia

Add Pinia only now that the course has established a real need for shared state:

```text
npm install pinia
```

Create one Pinia instance in `src/main.ts` and register it before mounting:

```ts
import { createPinia } from "pinia";

createApp(App).use(router).use(createPinia()).mount(root);
```

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```ts
import { defineStore } from "pinia";
import { ref } from "vue";
export const useCartStore = defineStore("cart", () => {
  const itemIds = ref<string[]>([]);
  function add(id: string) { if (!itemIds.value.includes(id)) itemIds.value.push(id); }
  return { itemIds, add };
});
```

## Common mistake

Do not create one store for every value or let components mutate unrelated store details freely.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 21](../21-async-components-loading-error-and-empty-states/README.md).
