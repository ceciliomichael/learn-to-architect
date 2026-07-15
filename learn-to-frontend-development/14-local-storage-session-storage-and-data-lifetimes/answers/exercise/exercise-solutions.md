# Exercise Solution: Local Storage, Session Storage, and Data Lifetimes

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

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

