# Exercise Solution: JSON Boundaries and Runtime Validation

```ts
type Product = {
  readonly id: string;
  readonly name: string;
  readonly priceCents: number;
};

function parseProduct(value: unknown): Product {
  if (typeof value !== "object" || value === null) {
    throw new Error("Product must be an object");
  }

  const record = value as Record<string, unknown>;
  if (
    typeof record.id !== "string" ||
    typeof record.name !== "string" ||
    !Number.isSafeInteger(record.priceCents) ||
    (record.priceCents as number) < 0
  ) {
    throw new Error("Invalid product");
  }

  return {
    id: record.id,
    name: record.name.trim(),
    priceCents: record.priceCents as number,
  };
}
```

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

