# Exercise Solution: Server Functions, Server Actions, and Mutations

```tsx
"use server";
export async function renameProject(formData: FormData) {
  const session = await requireSession();
  const name = parseProjectName(formData.get("name"));
  await updateOwnedProject(session.userId, name);
}
```

## Why this works

A server function runs trusted server code, and a server action can be invoked as a mutation endpoint from the UI. Validate input and authenticate and authorize every call. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.