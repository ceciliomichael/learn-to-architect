# Module 28: Discriminated Unions and State

## Before you start

Complete Modules 01 to 27. You should understand literal unions, object types, narrowing, and async result states.

## What you will learn

- connect object shapes with a shared literal property
- prevent impossible combinations of state properties
- narrow with `if` and `switch`
- check exhaustiveness with `never`
- define state transitions as functions

## Why this matters

Several optional properties can allow confusing combinations. A discriminated union gives each state exactly the data it needs.

## 1. The optional-property problem

```typescript
interface LoadState {
  isLoading: boolean;
  data?: string[];
  error?: string;
}
```

This permits unclear values:

```typescript
const confusing: LoadState = {
  isLoading: true,
  data: ["already loaded"],
  error: "also failed",
};
```

The type does not connect the flags to the available properties.

## 2. Give each state its own shape

```typescript
type LoadState =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: string[] }
  | { status: "error"; error: string };
```

`status` is the discriminant. Each member has one exact literal status.

Invalid combinations are rejected:

```typescript
// Intentional error: loading has no data property.
const invalid: LoadState = { status: "loading", data: [] };
```

## 3. Narrow by the discriminant

```typescript
function renderState(state: LoadState): string {
  if (state.status === "success") {
    return `Loaded ${state.data.length} items`;
  }

  if (state.status === "error") {
    return `Failed: ${state.error}`;
  }

  if (state.status === "loading") {
    return "Loading";
  }

  return "Ready";
}
```

TypeScript connects each literal to its member-specific properties.

## 4. Switch by state

```typescript
function renderState(state: LoadState): string {
  switch (state.status) {
    case "idle":
      return "Ready";
    case "loading":
      return "Loading";
    case "success":
      return `Loaded ${state.data.length} items`;
    case "error":
      return `Failed: ${state.error}`;
  }
}
```

When every member returns, TypeScript knows the function always produces a string.

## 5. Exhaustiveness with `never`

Add a helper:

```typescript
function assertNever(value: never): never {
  throw new Error(`Unhandled state: ${JSON.stringify(value)}`);
}
```

Use it in a default branch:

```typescript
function renderState(state: LoadState): string {
  switch (state.status) {
    case "idle":
      return "Ready";
    case "loading":
      return "Loading";
    case "success":
      return `Loaded ${state.data.length} items`;
    case "error":
      return `Failed: ${state.error}`;
    default:
      return assertNever(state);
  }
}
```

After all members are handled, `state` has type `never`, meaning no value should remain. If a new union member is added without a switch case, the call becomes a type error.

The runtime throw is still useful if unchecked data reaches this code.

## 6. Model events and transitions

```typescript
type Event =
  | { type: "load" }
  | { type: "succeed"; data: string[] }
  | { type: "fail"; error: string }
  | { type: "reset" };

function transition(state: LoadState, event: Event): LoadState {
  switch (event.type) {
    case "load":
      return { status: "loading" };
    case "succeed":
      return { status: "success", data: event.data };
    case "fail":
      return { status: "error", error: event.error };
    case "reset":
      return { status: "idle" };
    default:
      return assertNever(event);
  }
}
```

This simple function makes changes explicit. A stricter model could also reject events that are invalid for a particular current state.

## 7. Validate external discriminated data

The union is still static. If state arrives from storage or a server, validate the discriminant and the matching member properties before treating it as `LoadState`.

## Common mistakes

### Using a broad `status: string`

The discriminant needs exact literal types.

### Keeping unrelated optional fields on every member

Place data only on the state that owns it.

### Casting in the switch

Correct discriminants should narrow without assertions.

### Adding `assertNever` without handling runtime input boundaries

Exhaustive static checking does not validate external data.

## Check your understanding

1. What makes a union discriminated?
2. How does it prevent impossible property combinations?
3. What is `never` after exhaustive narrowing?
4. What happens when a new member is added but no case handles it?
5. Does a discriminated union validate stored JSON?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 29](../29-advanced-function-apis/README.md) designs flexible call signatures without losing clarity.
