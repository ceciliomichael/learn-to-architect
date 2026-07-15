# Exercise Solution: Composables and Reusable Stateful Logic

```ts
import { onUnmounted, ref } from "vue";
export function useClock() {
  const now = ref(new Date());
  const timer = window.setInterval(() => { now.value = new Date(); }, 1000);
  onUnmounted(() => window.clearInterval(timer));
  return { now };
}
```

## Why this works

A composable is a function that uses Vue reactivity to reuse stateful behavior. Each call owns its state unless a shared owner is intentionally defined. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.