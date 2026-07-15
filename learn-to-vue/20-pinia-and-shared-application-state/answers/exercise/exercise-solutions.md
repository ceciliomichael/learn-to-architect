# Exercise Solution: Pinia and Shared Application State

```ts
import { defineStore } from "pinia";
import { ref } from "vue";
export const useCartStore = defineStore("cart", () => {
  const itemIds = ref<string[]>([]);
  function add(id: string) { if (!itemIds.value.includes(id)) itemIds.value.push(id); }
  return { itemIds, add };
});
```

## Why this works

Pinia stores shared application state and actions when ownership truly spans distant components. Keep local component state local and expose focused store APIs. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.