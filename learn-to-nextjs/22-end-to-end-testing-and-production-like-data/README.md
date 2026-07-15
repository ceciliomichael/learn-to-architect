# Module 22: End-to-End Testing and Production-Like Data

## What you will learn

End-to-end tests exercise a built application through real user flows with controlled production-like test data and reliable cleanup.

## Initialize Playwright

Run the official initializer inside `nextjs-course`:

```text
npm init playwright@latest
```

Choose TypeScript, use `e2e` as the test directory, and install browser binaries. Configure Playwright's `webServer` to run the built application for release checks. Confirm the generated example works with `npx playwright test` before replacing it.

## How to reason about it

- Keep rendering and calculation separate from external I/O unless the lesson explicitly introduces that boundary.
- Treat props, route values, browser data, form values, server results, and stored data according to their real runtime trust level.
- Preserve semantic HTML, keyboard operation, visible focus, loading feedback, empty states, errors, and recovery while adding framework behavior.
- Give every stateful task an owner for completion, cancellation, cleanup, and user-visible failure.
- Verify behavior through strict types, browser evidence, and tests instead of relying on a screenshot.

## Complete focused example

```tsx
import { test, expect } from "@playwright/test";
test("creates a project", async ({ page }) => {
  await page.goto("/projects/new");
  await page.getByLabel("Name").fill("Garden");
  await page.getByRole("button", { name: "Create" }).click();
  await expect(page.getByRole("heading", { name: "Garden" })).toBeVisible();
});
```

## Common mistake

Do not make tests depend on shared mutable accounts, arbitrary delays, or a development-only runtime.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 23](../23-accessibility-security-headers-and-untrusted-content/README.md).
