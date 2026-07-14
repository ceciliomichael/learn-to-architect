# Exercise Solution: Accessibility, Security, and Measured Performance

```vue
<script setup lang="ts">
defineProps<{ message: string }>();
</script>
<template><p role="status">{{ message }}</p></template>
```

## Why this works

Preserve semantic HTML and focus, treat runtime content as untrusted, avoid raw HTML, measure rendering before optimizing, and keep reactive work close to its owner. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.