# Exercise Solution: DOM Integration and End-to-End Testing

```ts
// Framework-neutral test shape:
document.body.innerHTML = `
  <form id="signup">
    <label for="name">Name</label>
    <input id="name" name="name" required>
    <button>Join</button>
  </form>
`;

const button = document.querySelector("button");
if (!(button instanceof HTMLButtonElement)) throw new Error("Missing button");
button.click();
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

