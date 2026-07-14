# Exercise Solution: Refs, Reactive Objects, and Automatic Unwrapping

```vue
<script setup lang="ts">
import { reactive, ref } from "vue";
const count = ref(0);
const profile = reactive({ name: "Ada" });
</script>
<template><button @click="count++">{{ profile.name }}: {{ count }}</button></template>
```

## Why this works

A ref owns one reactive value and a reactive object tracks its properties. Templates unwrap refs for convenient reading, while TypeScript code normally uses value. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.