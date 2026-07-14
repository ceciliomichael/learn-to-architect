# Exercise Solution: Timers, Animation Frames, and Observer APIs

```ts
const output = document.querySelector("#clock");
if (!(output instanceof HTMLElement)) throw new Error("Missing clock");

const controller = new AbortController();
const timer = window.setInterval(() => {
  output.textContent = new Date().toLocaleTimeString();
}, 1_000);

controller.signal.addEventListener("abort", () => {
  window.clearInterval(timer);
}, { once: true });
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

