# Exercise Solution: Native Validation, Custom Rules, and Accessible Errors

```ts
const email = document.querySelector<HTMLInputElement>("#email");
const error = document.querySelector<HTMLParagraphElement>("#email-error");

if (email === null || error === null) throw new Error("Missing form UI");

email.addEventListener("input", () => {
  const allowed = email.value.endsWith("@example.test");
  email.setCustomValidity(allowed ? "" : "Use your example.test address.");
  email.setAttribute("aria-invalid", String(!allowed));
  error.textContent = allowed ? "" : "Use your example.test address.";
});
```

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

