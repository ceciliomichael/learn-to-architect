# Exercise Solution: Error States, Logging, and User Recovery

```ts
function showLoadFailure(container: HTMLElement, retry: () => void): void {
  const message = document.createElement("p");
  message.textContent = "Products could not be loaded.";

  const button = document.createElement("button");
  button.type = "button";
  button.textContent = "Try again";
  button.addEventListener("click", retry, { once: true });

  container.replaceChildren(message, button);
}
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

