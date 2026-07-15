# Exercise Solution: Single-File Components and script setup

```vue
<script setup lang="ts">
const title = "Welcome";
</script>

<template>
  <h1>{{ title }}</h1>
</template>
```

## Why this works

A Single-File Component keeps one component template, logic, and scoped presentation together. script setup exposes its top-level bindings directly to that component template. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.