# Module 21: Errors and Recovery

## Before you start

Complete Modules 01 to 20. You should understand unknown data, validation, and discriminating object shapes with properties.

## What you will learn

- distinguish expected failure from unexpected failure
- throw and catch an `Error`
- handle caught values as `unknown`
- use `finally` for cleanup that must be attempted
- return a result union for expected failure
- avoid losing useful error context

## Why this matters

Files can be missing, JSON can be malformed, and input can be invalid. A reliable program makes failure paths visible and gives callers enough information to respond.

## 1. Some failures are expected outcomes

An invalid form field is expected and should usually be returned as ordinary data. A broken invariant or unavailable required resource may justify throwing an error.

Ask:

- Can the caller reasonably recover here?
- Is failure part of normal use?
- Does the current function have enough context to solve it?

Use a returned result for expected alternatives. Use thrown errors for exceptional failure that interrupts normal flow.

## 2. Throw an `Error` object

```typescript
function divide(left: number, right: number): number {
  if (right === 0) {
    throw new Error("Cannot divide by zero");
  }

  return left / right;
}
```

`throw` stops normal execution and looks for a surrounding error handler. Throw `Error` objects rather than plain strings because they carry a message and stack information.

## 3. Catch unknown errors

```typescript
try {
  console.log(divide(10, 0));
} catch (error: unknown) {
  if (error instanceof Error) {
    console.log(`Operation failed: ${error.message}`);
  } else {
    console.log("Operation failed with an unknown value");
  }
}
```

JavaScript permits throwing any value, so a caught value should be treated as unknown. `instanceof Error` is a runtime check that narrows it.

## 4. Use `finally` for cleanup attempts

```typescript
try {
  console.log("Start operation");
  throw new Error("Operation failed");
} catch (error: unknown) {
  console.log("Handle failure");
} finally {
  console.log("Release temporary resource");
}
```

The `finally` block runs whether the try block completes or throws, including when the catch returns. Use it for cleanup such as closing a resource. Avoid returning from `finally`, because that can replace an earlier result or thrown error.

## 5. Catch errors where you can respond

Do not catch an error only to ignore it:

```typescript
try {
  riskyOperation();
} catch {
  // Failure disappears.
}
```

A useful handler might:

- show a clear message
- retry when appropriate
- add context and rethrow
- choose a safe fallback
- return an expected failure result

Do not log private data or secrets while adding context.

## 6. A result union for expected failure

Before generics, create a result for one operation:

```typescript
type ParseNumberResult =
  | { ok: true; value: number }
  | { ok: false; error: string };

function parseWholeNumber(text: string): ParseNumberResult {
  const value = Number(text);

  if (!Number.isInteger(value)) {
    return { ok: false, error: "Enter a whole number" };
  }

  return { ok: true, value };
}
```

Handle both paths:

```typescript
const result = parseWholeNumber("12");

if (result.ok) {
  console.log(result.value);
} else {
  console.log(result.error);
}
```

The `ok` property is a discriminant. Its exact boolean value connects each branch to its matching properties.

## 7. Safely parse JSON

```typescript
type JsonResult =
  | { ok: true; value: unknown }
  | { ok: false; error: string };

function parseJson(text: string): JsonResult {
  try {
    const value: unknown = JSON.parse(text);
    return { ok: true, value };
  } catch (error: unknown) {
    if (error instanceof Error) {
      return { ok: false, error: error.message };
    }

    return { ok: false, error: "Unknown JSON parsing error" };
  }
}
```

Successful parsing proves only that the text is valid JSON. The returned value is still unknown and needs shape validation.

## 8. Preserve error context

If a low-level message lacks meaning, add context:

```typescript
try {
  loadSettings();
} catch (error: unknown) {
  if (error instanceof Error) {
    throw new Error(`Could not load application settings: ${error.message}`, {
      cause: error,
    });
  }

  throw new Error("Could not load application settings", { cause: error });
}
```

The `cause` option preserves the original failure for debugging in supported modern runtimes.

## Common mistakes

### Treating every invalid input as an exception

Normal user correction is often clearer as a returned result.

### Assuming caught values are always `Error`

Narrow from unknown.

### Swallowing an error

Handle, translate, or rethrow it with purpose.

### Returning from `finally`

It can hide the original result or error.

## Check your understanding

1. When is a returned result useful?
2. Why throw an `Error` rather than a string?
3. Why is a caught value treated as unknown?
4. When does `finally` run?
5. Does successful JSON parsing prove a particular object shape?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 22](../22-generics/README.md) turns operation-specific containers such as results into reusable type-safe patterns.
