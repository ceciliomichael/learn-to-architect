# Exercise Solution: Computed Values and Derived State

```vue
<script setup lang="ts">
import { computed, ref } from "vue";
const first = ref("Ada");
const last = ref("Lovelace");
const fullName = computed(() => `${first.value} ${last.value}`);
</script>
<template><p>{{ fullName }}</p></template>
```

## Why this works

A computed value derives information from reactive sources and should stay pure, cached by dependency, and free of mutation. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.