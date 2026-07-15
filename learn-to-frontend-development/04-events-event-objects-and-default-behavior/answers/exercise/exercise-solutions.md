# Exercise Solution: Events, Event Objects, and Default Behavior

```ts
const form = document.querySelector<HTMLFormElement>("#search-form");
if (form === null) throw new Error("Expected search form");

form.addEventListener("submit", (event) => {
  event.preventDefault();
  const data = new FormData(form);
  const query = data.get("query");

  if (typeof query === "string") {
    console.log(query.trim());
  }
});
```

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

