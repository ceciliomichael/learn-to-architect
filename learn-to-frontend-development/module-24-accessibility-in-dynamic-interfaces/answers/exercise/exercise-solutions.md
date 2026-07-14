# Exercise Solution: Accessibility in Dynamic Interfaces

```ts
const status = document.querySelector<HTMLParagraphElement>("#save-status");
const save = document.querySelector<HTMLButtonElement>("#save");
if (status === null || save === null) throw new Error("Missing save UI");

save.addEventListener("click", async () => {
  save.disabled = true;
  status.textContent = "Saving";
  try {
    await Promise.resolve();
    status.textContent = "Saved";
  } finally {
    save.disabled = false;
  }
});
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

