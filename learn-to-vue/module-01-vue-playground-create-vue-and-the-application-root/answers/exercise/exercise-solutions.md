# Exercise Solution: Vue Playground, create-vue, and the Application Root

```ts
import { createApp } from "vue";
import App from "./App.vue";
const root = document.querySelector("#app");
if (root === null) throw new Error("Missing #app");
createApp(App).mount(root);
```

## Why this works

Use the official playground for a quick experiment or create-vue for a local strict TypeScript project, then identify the application root and the component mounted into it. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.