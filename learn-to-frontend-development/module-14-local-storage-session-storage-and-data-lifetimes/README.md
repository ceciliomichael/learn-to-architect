# Module 14: Local Storage, Session Storage, and Data Lifetimes

## What you will learn

Store small non-secret preferences with explicit versioning and failure handling.

## Contracts to understand

- No. It can be old, edited, corrupted, or written by another script on the origin.
- It persists by origin until cleared or evicted, unlike sessionStorage's tab session lifetime.
- No. Origin scripts can read it, and users or extensions may inspect it.
- Stored shapes outlive deployments and need explicit migration or rejection.
- Yes, due to policy, quota, privacy mode, or unavailable storage.

## Complete TypeScript example

```ts
type Preferences = { readonly theme: "light" | "dark" };
const key = "garden.preferences.v1";

function savePreferences(value: Preferences): void {
  try {
    localStorage.setItem(key, JSON.stringify(value));
  } catch {
    console.warn("Preferences could not be saved");
  }
}

function loadPreferences(): Preferences | null {
  const text = localStorage.getItem(key);
  if (text === null) return null;
  try {
    const value: unknown = JSON.parse(text);
    if (
      typeof value === "object" &&
      value !== null &&
      "theme" in value &&
      (value.theme === "light" || value.theme === "dark")
    ) return { theme: value.theme };
  } catch {}
  localStorage.removeItem(key);
  return null;
}
```

Type-check with strict DOM settings, run in the course browser project, and inspect the relevant developer-tool panel. Do not use a type assertion to replace missing runtime evidence.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md), then compare the [exercise solution](answers/exercise/exercise-solutions.md) and [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 15](../module-15-cookies-credentials-and-server-controlled-sessions/README.md).

