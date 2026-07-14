# Exercise Solution: Forms and v-model

```vue
<script setup lang="ts">
import { ref } from "vue";
const name = ref("");
</script>
<template><label>Name <input v-model.trim="name" required /></label><p>Hello, {{ name || "learner" }}.</p></template>
```

## Why this works

v-model connects a form control value and its update event, but each control type still follows native HTML semantics and needs a label, validation, and an error path. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.