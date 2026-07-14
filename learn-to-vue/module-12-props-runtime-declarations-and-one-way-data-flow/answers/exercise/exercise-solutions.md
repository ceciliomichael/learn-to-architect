# Exercise Solution: Props, Runtime Declarations, and One-Way Data Flow

```vue
<script setup lang="ts">
const props = defineProps<{ title: string; count?: number }>();
</script>
<template><h2>{{ props.title }} ({{ props.count ?? 0 }})</h2></template>
```

## Why this works

Props are one-way readonly inputs. Type declarations help authors, runtime declarations can validate JavaScript callers, and object or array defaults must not be shared mutable instances. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.