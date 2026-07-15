# Exercise Solution: Component Events and Typed Emits

```vue
<script setup lang="ts">
const emit = defineEmits<{ save: [name: string] }>();
</script>
<template><button type="button" @click="emit(`save`, `Ada`)">Save Ada</button></template>
```

## Why this works

A child emits a named event with a typed payload and the parent decides how application state changes. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.