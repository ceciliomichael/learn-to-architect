# Exercise Solution: Component Registration and Composition

```vue
<script setup lang="ts">
import PageTitle from "./PageTitle.vue";
</script>
<template><main><PageTitle /><p>Choose a lesson.</p></main></template>
```

## Why this works

Import and compose small components so each component owns one understandable part of the interface and communicates through explicit inputs and outputs. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.