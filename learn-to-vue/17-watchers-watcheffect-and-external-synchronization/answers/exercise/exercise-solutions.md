# Exercise Solution: Watchers, watchEffect, and External Synchronization

```ts
import { ref, watch } from "vue";
const query = ref("");
watch(query, async (value, _oldValue, onCleanup) => {
  const controller = new AbortController();
  onCleanup(() => controller.abort());
  results.value = await search(value, controller.signal);
});
```

## Why this works

Use watch for a chosen reactive source and watchEffect for automatically tracked synchronization. Invalidate or clean up stale asynchronous work whenever dependencies change. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.