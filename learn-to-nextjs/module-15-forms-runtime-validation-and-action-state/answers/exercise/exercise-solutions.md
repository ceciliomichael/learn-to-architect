# Exercise Solution: Forms, Runtime Validation, and Action State

```tsx
"use client";
import { useActionState } from "react";
export function NameForm({ action }: { action: (state: FormState, data: FormData) => Promise<FormState> }) {
  const [state, formAction, pending] = useActionState(action, { error: "" });
  return <form action={formAction}><label>Name <input name="name" required /></label><p role="alert">{state.error}</p><button disabled={pending}>{pending ? "Saving..." : "Save"}</button></form>;
}
```

## Why this works

Forms should work with browser semantics first, validate on the server, preserve entered values when useful, and expose pending and field errors through accessible action state. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.