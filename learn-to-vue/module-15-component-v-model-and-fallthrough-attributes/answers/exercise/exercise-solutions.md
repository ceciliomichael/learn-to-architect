# Exercise Solution: Component v-model and Fallthrough Attributes

```vue
<script setup lang="ts">
const model = defineModel<string>({ required: true });
</script>
<template><label>Name <input v-model="model" /></label></template>
```

## Why this works

Component v-model is a prop and update event contract, while fallthrough attributes let a wrapper preserve useful HTML attributes and listeners on the intended root element. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.