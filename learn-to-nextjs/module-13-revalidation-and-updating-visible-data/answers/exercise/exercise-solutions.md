# Exercise Solution: Revalidation and Updating Visible Data

```tsx
import { revalidatePath } from "next/cache";
export async function saveItem(input: ItemInput) {
  await database.transaction(() => insertItem(input));
  revalidatePath("/items");
}
```

## Why this works

After a successful mutation, update or invalidate the cached view that represents the changed data so the next render tells the truth. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.