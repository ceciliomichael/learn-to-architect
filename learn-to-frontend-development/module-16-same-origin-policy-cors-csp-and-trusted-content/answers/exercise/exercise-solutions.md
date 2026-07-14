# Exercise Solution: Same-Origin Policy, CORS, CSP, and Trusted Content

```ts
const status = document.querySelector("#status");
if (!(status instanceof HTMLElement)) throw new Error("Missing status");

function showMessage(message: string): void {
  status.textContent = message;
}

showMessage(new URL(location.href).searchParams.get("message") ?? "Ready");
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

