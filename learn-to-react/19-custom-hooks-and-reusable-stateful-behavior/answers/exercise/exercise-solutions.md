# Exercise Solution: Custom Hooks and Reusable Stateful Behavior

```tsx
import { useSyncExternalStore } from "react";
function subscribe(callback: () => void) {
  window.addEventListener("online", callback);
  window.addEventListener("offline", callback);
  return () => { window.removeEventListener("online", callback); window.removeEventListener("offline", callback); };
}
function getSnapshot() { return navigator.onLine; }
function getServerSnapshot() { return true; }
export function useOnlineStatus() {
  return useSyncExternalStore(subscribe, getSnapshot, getServerSnapshot);
}
```

## Why this works

A custom hook reuses stateful behavior and follows Hook call rules while each caller retains independent state. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.