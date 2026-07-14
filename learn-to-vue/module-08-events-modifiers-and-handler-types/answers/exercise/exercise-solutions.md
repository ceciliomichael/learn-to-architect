# Exercise Solution: Events, Modifiers, and Handler Types

```vue
<script setup lang="ts">
function save(event: MouseEvent) {
  console.log("Saved from", event.currentTarget);
}
</script>
<template><button type="button" @click="save">Save</button></template>
```

## Why this works

Event bindings receive browser events or call named handlers, and modifiers express common DOM behavior close to the binding. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.