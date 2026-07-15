# Exercise Solution: End-to-End Testing and Production-Like Data

```tsx
import { test, expect } from "@playwright/test";
test("creates a project", async ({ page }) => {
  await page.goto("/projects/new");
  await page.getByLabel("Name").fill("Garden");
  await page.getByRole("button", { name: "Create" }).click();
  await expect(page.getByRole("heading", { name: "Garden" })).toBeVisible();
});
```

## Why this works

End-to-end tests exercise a built application through real user flows with controlled production-like test data and reliable cleanup. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.