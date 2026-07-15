# Exercise Solution: Create and Trace a React Application

## Commands

```text
npm create vite@latest react-course -- --template react-ts
cd react-course
npm install
npm run dev
```

## index.html

Keep the generated document and make sure it contains these entries:

```html
<title>React Study Planner</title>
<div id="root"></div>
<script type="module" src="/src/main.tsx"></script>
```

## src/main.tsx

```tsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./index.css";
import App from "./App";

const container = document.getElementById("root");

if (container === null) {
  throw new Error("Expected an element with id root");
}

createRoot(container).render(
  <StrictMode>
    <App />
  </StrictMode>,
);
```

## src/App.tsx

```tsx
export default function App() {
  return (
    <main>
      <h1>React Study Planner</h1>
      <p>I want to understand components instead of copying them.</p>
      <p>This application is mounted into the root element.</p>
    </main>
  );
}
```

## Final checks

```text
npm run lint
npm run build
```

`index.html` supplies the real DOM container and loads `src/main.tsx`. That file validates the container, creates the React root, and renders `<App />`. `src/App.tsx` defines the visible application tree.
