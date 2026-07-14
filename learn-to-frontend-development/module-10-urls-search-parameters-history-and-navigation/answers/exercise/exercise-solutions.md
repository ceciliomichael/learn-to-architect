# Exercise Solution: URLs, Search Parameters, History, and Navigation

```ts
const url = new URL(window.location.href);
url.searchParams.set("topic", "compost");
url.searchParams.set("page", "2");

history.pushState({ topic: "compost" }, "", url);

window.addEventListener("popstate", () => {
  const current = new URL(window.location.href);
  console.log(current.searchParams.get("topic"));
});
```

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

