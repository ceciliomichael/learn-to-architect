# Exercise Solution: Template Syntax and Safe Expressions

```vue
<script setup lang="ts">
const learner = { name: "Ada", lessons: 3 };
</script>
<template><p>{{ learner.name }} has {{ learner.lessons }} lessons.</p></template>
```

## Why this works

Vue templates are HTML-like declarations with directives and JavaScript expressions. Interpolation escapes text, while directives control attributes and behavior. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.