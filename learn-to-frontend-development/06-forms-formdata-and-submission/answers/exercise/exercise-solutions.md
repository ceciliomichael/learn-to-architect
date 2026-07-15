# Exercise Solution: Forms, FormData, and Submission

```ts
const form = document.querySelector<HTMLFormElement>("#registration");
if (form === null) throw new Error("Expected registration form");

form.addEventListener("submit", (event) => {
  event.preventDefault();
  const data = new FormData(form);
  const name = data.get("fullName");
  const topics = data.getAll("topics");

  if (typeof name !== "string") return;
  console.log({ name: name.trim(), topics });
});
```

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

