# Exercise Solution: Lifecycle Hooks and Template Refs

```vue
<script setup lang="ts">
import { onMounted, onUnmounted, useTemplateRef } from "vue";
const field = useTemplateRef<HTMLInputElement>("field");
let timer = 0;
onMounted(() => { field.value?.focus(); timer = window.setInterval(() => {}, 1000); });
onUnmounted(() => window.clearInterval(timer));
</script>
<template><input ref="field" aria-label="Search" /></template>
```

## Why this works

Lifecycle hooks schedule work around component mounting and removal, while template refs provide limited DOM access after mounting. Clean up every owned external resource. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.