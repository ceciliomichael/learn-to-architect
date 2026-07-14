# Module 28 Exercise Solutions

## Exercises 1 and 2

```typescript
type SaveState =
  | { status: "idle" }
  | { status: "saving" }
  | { status: "saved"; savedAt: Date }
  | { status: "failed"; error: string };

function assertNever(value: never): never {
  throw new Error(`Unhandled value: ${JSON.stringify(value)}`);
}

function renderSave(state: SaveState): string {
  switch (state.status) {
    case "idle":
      return "Ready";
    case "saving":
      return "Saving";
    case "saved":
      return `Saved at ${state.savedAt.toISOString()}`;
    case "failed":
      return `Failed: ${state.error}`;
    default:
      return assertNever(state);
  }
}
```

Adding another member makes the default call fail to type-check until a case removes that member.

## Exercise 3

```typescript
type SaveEvent =
  | { type: "start" }
  | { type: "succeed"; savedAt: Date }
  | { type: "fail"; error: string }
  | { type: "reset" };

function transitionSave(event: SaveEvent): SaveState {
  switch (event.type) {
    case "start": return { status: "saving" };
    case "succeed": return { status: "saved", savedAt: event.savedAt };
    case "fail": return { status: "failed", error: event.error };
    case "reset": return { status: "idle" };
    default: return assertNever(event);
  }
}
```

## Exercise 4

```typescript
type FormState =
  | { status: "editing" }
  | { status: "submitting" }
  | { status: "submitted"; receiptId: string }
  | { status: "failed"; error: string };
```

## Exercise 5

The JSON value exists outside static checking. It may omit required properties. Validate both the discriminant and the properties required for that member.
