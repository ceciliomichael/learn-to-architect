# Exercise Solution: Authorization in Pages, Actions, and Route Handlers

```tsx
export async function deleteProject(projectId: string, userId: string) {
  const project = await findProject(projectId);
  if (project === null || project.ownerId !== userId) throw new Error("Not allowed");
  await removeProject(projectId);
}
```

## Why this works

Authorization decides whether the authenticated identity may perform this exact operation on this exact resource. Enforce it beside every protected read and write. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.