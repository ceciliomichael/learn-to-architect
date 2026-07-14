# Exercise Solution: The DOM Tree and Safe Element Queries

```ts
function requireElement<T extends Element>(
  selector: string,
  expected: { new (...args: never[]): T },
): T {
  const element = document.querySelector(selector);
  if (!(element instanceof expected)) {
    throw new Error(`Expected ${selector}`);
  }
  return element;
}

const heading = requireElement("#page-title", HTMLHeadingElement);
console.log(heading.textContent);
```

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

