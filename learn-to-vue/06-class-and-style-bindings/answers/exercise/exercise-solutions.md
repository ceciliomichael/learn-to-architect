# Exercise Solution: Class and Style Bindings

```vue
<script setup lang="ts">
import { ref } from "vue";
const active = ref(false);
</script>
<template><button :class="{ active }" :aria-pressed="active" @click="active = !active">Notifications</button></template>
```

## Why this works

Class and style bindings can combine fixed presentation with reactive state while keeping the state meaning separate from CSS details. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.