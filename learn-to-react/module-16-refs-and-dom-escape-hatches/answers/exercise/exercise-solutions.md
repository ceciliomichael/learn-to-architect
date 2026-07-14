# Exercise Solution: Refs and DOM Escape Hatches

```tsx
import { useRef } from "react";
export function SearchField() {
  const inputRef = useRef<HTMLInputElement>(null);
  return <><input ref={inputRef} aria-label="Search" /><button type="button" onClick={() => inputRef.current?.focus()}>Focus search</button></>;
}
```

## Why this works

Refs hold values that do not drive rendering and provide deliberate access to DOM escape hatches. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.