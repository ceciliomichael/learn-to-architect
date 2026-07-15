# Exercise Solution: Conditional and List Rendering with Stable Keys

```vue
<script setup lang="ts">
const tasks = [{ id: "read", label: "Read lesson" }];
</script>
<template><p v-if="tasks.length === 0">No tasks.</p><ul v-else><li v-for="task in tasks" :key="task.id">{{ task.label }}</li></ul></template>
```

## Why this works

Use v-if when content should exist conditionally, v-show for frequent visibility changes, and v-for with a stable key derived from item identity. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.