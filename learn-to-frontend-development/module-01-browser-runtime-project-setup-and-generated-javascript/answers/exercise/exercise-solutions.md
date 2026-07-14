# Exercise Solution: Browser Runtime, Project Setup, and Generated JavaScript

```ts
const message: string = "Browser TypeScript is running.";
const output = document.querySelector<HTMLParagraphElement>("#output");

if (output === null) {
  throw new Error("Expected #output");
}

output.textContent = message;
```

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

