# Exercise Solution: Unit Testing Browser Logic

```ts
export type State = { readonly count: number };

export function reduce(
  state: State,
  action: "increment" | "reset",
): State {
  if (action === "reset") return { count: 0 };
  return { count: state.count + 1 };
}

// Test expectations:
// reduce({ count: 2 }, "increment") equals { count: 3 }
// reduce({ count: 2 }, "reset") equals { count: 0 }
```

## Why this works

The reference keeps browser I/O, runtime validation, lifecycle ownership, and user recovery explicit. Adaptations are correct when they preserve those contracts and observable behavior.

