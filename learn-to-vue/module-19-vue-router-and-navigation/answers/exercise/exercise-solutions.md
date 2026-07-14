# Exercise Solution: Vue Router and Navigation

```ts
import { createRouter, createWebHistory } from "vue-router";
export const router = createRouter({
  history: createWebHistory(),
  routes: [{ path: "/", component: () => import("./views/HomeView.vue") }]
});
```

## Why this works

Vue Router maps URLs to views, preserves real links, parses route values as untrusted input, and supports nested layouts and navigation guards. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.