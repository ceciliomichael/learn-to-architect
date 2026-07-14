# Exercise Solution: Slots and Content Composition

```vue
<template><section><header><slot name="title" /></header><div><slot /></div></section></template>
```

## Why this works

Slots let a parent supply content while the child owns surrounding structure, and named or scoped slots make those responsibilities explicit. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.