# Exercise Solution: React Playground, Local Project, and Rendering Root

```tsx
import { createRoot } from "react-dom/client";
import { StrictMode } from "react";
import App from "./App";
const root = document.getElementById("root");
if (root === null) throw new Error("Missing #root");
createRoot(root).render(<StrictMode><App /></StrictMode>);
```

## Why this works

Start in an official sandbox or a local strict TypeScript project, identify the DOM root, and render one application tree. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.