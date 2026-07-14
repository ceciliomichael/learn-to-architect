# Exercise Solution: Async Components, Loading, Error, and Empty States

```vue
<script setup lang="ts">
import { defineAsyncComponent } from "vue";
const ReportPanel = defineAsyncComponent({ loader: () => import("./ReportPanel.vue"), loadingComponent: () => import("./LoadingPanel.vue"), errorComponent: () => import("./ErrorPanel.vue") });
</script>
<template><ReportPanel /></template>
```

## Why this works

Async components can delay code loading, while data work needs explicit loading, empty, error, success, cancellation, and retry behavior. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.