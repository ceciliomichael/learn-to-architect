# Exercise Solution: Service Workers, Offline Behavior, and Update Safety

```ts
if ("serviceWorker" in navigator) {
  window.addEventListener("load", () => {
    void navigator.serviceWorker.register("/service-worker.js", {
      scope: "/",
    });
  });
}
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

