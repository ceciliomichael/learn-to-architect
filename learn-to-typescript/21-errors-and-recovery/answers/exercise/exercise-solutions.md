# Module 21 Exercise Solutions

## Exercise 1

```typescript
function getItemAt(items: readonly string[], index: number): string {
  const item = items[index];

  if (item === undefined) {
    throw new Error(`No item exists at index ${index}`);
  }

  return item;
}

try {
  console.log(getItemAt(["a"], 2));
} catch (error: unknown) {
  if (error instanceof Error) {
    console.log(error.message);
  }
}
```

## Exercise 2

```typescript
type PositiveNumberResult =
  | { ok: true; value: number }
  | { ok: false; error: string };

function validatePositive(value: number): PositiveNumberResult {
  if (value <= 0) {
    return { ok: false, error: "Value must be greater than zero" };
  }

  return { ok: true, value };
}
```

## Exercise 3

```typescript
type JsonResult =
  | { ok: true; value: unknown }
  | { ok: false; error: string };

function parseJson(text: string): JsonResult {
  try {
    const value: unknown = JSON.parse(text);
    return { ok: true, value };
  } catch (error: unknown) {
    const message = error instanceof Error ? error.message : "Unknown parsing error";
    return { ok: false, error: message };
  }
}
```

## Exercise 4

For success, `try` then `finally` print. For a caught failure, `try`, `catch`, then `finally` print. `finally` performs the cleanup attempt in both paths.

## Exercise 5

- Password rule failure is expected user input, so return a validation result.
- An impossible internal state can justify throwing because it breaks a programmer contract.
- No search match is usually an ordinary `undefined` or result outcome.
- A missing required startup file can justify throwing because the program cannot fulfill its purpose.

The right choice can vary with the caller. The explanation and recovery path matter more than a fixed slogan.
