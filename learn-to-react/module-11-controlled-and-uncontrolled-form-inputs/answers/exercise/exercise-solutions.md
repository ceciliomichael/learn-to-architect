# Exercise Solution: Controlled and Uncontrolled Form Inputs

```tsx
import { useState } from "react";
export function NameField() {
  const [name, setName] = useState("");
  return <label>Name <input value={name} onChange={event => setName(event.target.value)} /></label>;
}
```

## Why this works

Controlled inputs receive value and onChange from React state, while uncontrolled inputs keep current value in the DOM; choose deliberately. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.