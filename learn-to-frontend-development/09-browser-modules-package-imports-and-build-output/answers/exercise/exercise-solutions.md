# Exercise Solution: Browser Modules, Package Imports, and Build Output

```ts
// format-name.ts
export function formatName(value: string): string {
  return value.trim().replaceAll(/\s+/g, " ");
}

// main.ts
import { formatName } from "./format-name.js";

console.log(formatName("  Ada   Lovelace  "));
```

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

