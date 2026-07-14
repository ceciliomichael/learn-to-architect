# Module 20: Unknown Data and Runtime Validation

## Before you start

Complete Modules 01 to 19. Use the strict project configuration from Module 19.

## What you will learn

- identify boundaries where static knowledge ends
- use `unknown` for untrusted values
- narrow unknown primitives and objects
- write a reusable type guard
- validate parsed JSON before using it
- understand why assertions do not validate

## Why this matters

TypeScript checks code it can see. It cannot guarantee that a user, file, server, or older database sends the promised data. Runtime validation connects outside data to trusted internal types.

## 1. Types do not inspect arriving data

This annotation is only a claim:

```typescript
interface User {
  name: string;
  age: number;
}
```

If a server sends `{ "name": 42 }`, the interface does not repair or reject it. Code must check the real runtime value.

Useful boundaries include:

- parsed JSON
- network responses
- form or command-line input
- local storage
- environment variables
- messages from another process

## 2. `unknown` keeps uncertainty visible

```typescript
function printValue(value: unknown): void {
  // Intentional error: not every unknown value has this method.
  console.log(value.toUpperCase());
}
```

Narrow first:

```typescript
function printValue(value: unknown): void {
  if (typeof value === "string") {
    console.log(value.toUpperCase());
  }
}
```

`unknown` accepts any incoming value but permits few operations until checks provide evidence.

## 3. How `any` differs

`any` tells TypeScript to stop checking operations that flow through that value:

```typescript
let unchecked: any = "hello";
unchecked.missing.method();
```

The checker allows this chain, but runtime behavior can fail.

`any` can be useful during controlled migrations or when describing code that truly cannot be typed yet. It carries risk and can spread. At an uncertain boundary, prefer `unknown` because it requires a check.

## 4. Check for a non-null object

```typescript
function isObject(value: unknown): boolean {
  return typeof value === "object" && value !== null;
}
```

Remember that arrays also have runtime type `"object"`. If the function needs a plain property dictionary, exclude arrays.

```typescript
type UnknownRecord = {
  [key: string]: unknown;
};

function isUnknownRecord(value: unknown): value is UnknownRecord {
  return typeof value === "object" && value !== null && !Array.isArray(value);
}
```

The return type `value is UnknownRecord` is a type predicate. When this function returns true, TypeScript narrows the checked value to `UnknownRecord`.

## 5. Validate an object shape

```typescript
interface User {
  name: string;
  age: number;
}

function isUser(value: unknown): value is User {
  if (!isUnknownRecord(value)) {
    return false;
  }

  return typeof value["name"] === "string" && typeof value["age"] === "number";
}
```

This checks the requirements stated by `User`. It does not need to reject unrelated extra properties unless the application requires that rule.

Use it:

```typescript
function welcomeUser(value: unknown): string {
  if (!isUser(value)) {
    return "Invalid user data";
  }

  return `Welcome, ${value.name}`;
}
```

## 6. Validate parsed JSON

The standard typing of `JSON.parse` returns `any`, so immediately place the result in `unknown`:

```typescript
function parseUser(json: string): User | undefined {
  const parsed: unknown = JSON.parse(json);

  if (!isUser(parsed)) {
    return undefined;
  }

  return parsed;
}
```

Invalid JSON text causes `JSON.parse` to throw before validation. Module 21 handles that failure.

## 7. Validate arrays item by item

```typescript
function isStringArray(value: unknown): value is string[] {
  return Array.isArray(value) && value.every((item) => typeof item === "string");
}
```

Checking only `Array.isArray` proves that the value is an array, not that every item is a string.

## 8. Assertions are not validation

```typescript
const parsed = JSON.parse('{"name":42}') as User;
console.log(parsed.name.toUpperCase());
```

`as User` tells TypeScript to accept the programmer's claim. It emits no runtime check and does not change `42` into text. The method call fails.

Use an assertion when you genuinely have evidence TypeScript cannot express, not as a replacement for checking untrusted data.

## 9. Validation should return useful evidence

A boolean type guard is good when callers only need yes or no. A parser can return a result with error details when users need to correct input. Module 21 introduces that result shape.

For complex applications, a well-maintained validation library may reduce repetitive checks. The principle remains the same: runtime evidence must justify the static type.

## Common mistakes

### Annotating a network response and calling it validated

The annotation does not inspect the response.

### Checking only that a value is an object

Check required properties and their runtime types too.

### Forgetting `null` and arrays in object checks

Both need deliberate handling.

### Replacing every error with an assertion

Assertions can hide the exact boundary bug TypeScript was revealing.

## Check your understanding

1. Why does `unknown` require narrowing?
2. How does `any` affect checking?
3. Why must an object check exclude `null`?
4. What does a type predicate tell TypeScript?
5. Does `as User` validate or convert a runtime value?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 21](../21-errors-and-recovery/README.md) handles operations that may fail and preserves useful error information.
