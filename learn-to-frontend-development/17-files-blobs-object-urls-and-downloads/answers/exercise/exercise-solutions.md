# Exercise Solution: Files, Blobs, Object URLs, and Downloads

```ts
const input = document.querySelector<HTMLInputElement>("#photo");
const preview = document.querySelector<HTMLImageElement>("#preview");
if (input === null || preview === null) throw new Error("Missing file UI");

let currentUrl: string | null = null;
input.addEventListener("change", () => {
  const file = input.files?.[0];
  if (file === undefined || !file.type.startsWith("image/") || file.size > 2_000_000) return;

  if (currentUrl !== null) URL.revokeObjectURL(currentUrl);
  currentUrl = URL.createObjectURL(file);
  preview.src = currentUrl;
});
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

