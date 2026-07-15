# Exercise Solution: Cookies, Credentials, and Server-Controlled Sessions

```ts
async function loadAccount(): Promise<unknown> {
  const response = await fetch("/api/account", {
    credentials: "same-origin",
    headers: { Accept: "application/json" },
  });

  if (response.status === 401) return null;
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  return response.json();
}
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

