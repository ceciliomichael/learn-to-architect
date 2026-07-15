# Exercise Solution: Create and Trace a Vue Application

## Commands

```text
npm create vue@latest
cd vue-course
npm install
npm run dev
```

Choose TypeScript and ESLint. Leave the other optional features off.

## index.html

Keep the generated document and confirm these entries:

```html
<title>Vue Study Planner</title>
<div id="app"></div>
<script type="module" src="/src/main.ts"></script>
```

## src/main.ts

```ts
import "./assets/main.css";
import { createApp } from "vue";
import App from "./App.vue";

const root = document.querySelector("#app");

if (root === null) {
  throw new Error("Expected an element with id app");
}

createApp(App).mount(root);
```

## src/App.vue

```vue
<script setup lang="ts">
const projectName: string = "Vue Study Planner";
</script>

<template>
  <main>
    <h1>{{ projectName }}</h1>
    <p>I am learning where a Vue application begins.</p>
  </main>
</template>
```

## Final checks

```text
npm run lint
npm run type-check
npm run build
```

`index.html` supplies the mount element and loads `src/main.ts`. The entry file validates that element, creates the Vue application from `App`, and mounts it. `src/App.vue` defines the visible root component.
