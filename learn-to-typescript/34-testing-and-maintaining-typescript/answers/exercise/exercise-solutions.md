# Module 34 Exercise Solutions

## Exercise 1

```typescript
export function clamp(value: number, minimum: number, maximum: number): number {
  if (value < minimum) return minimum;
  if (value > maximum) return maximum;
  return value;
}
```

```typescript
test("clamp keeps and limits values", () => {
  assert.equal(clamp(5, 0, 10), 5);
  assert.equal(clamp(0, 0, 10), 0);
  assert.equal(clamp(10, 0, 10), 10);
  assert.equal(clamp(-1, 0, 10), 0);
  assert.equal(clamp(11, 0, 10), 10);
});
```

## Exercise 2

```typescript
function requireTitle(title: string): string {
  if (title.trim().length === 0) throw new Error("Title is required");
  return title;
}

test("requireTitle rejects empty text", () => {
  assert.throws(() => requireTitle("  "), /Title is required/);
  assert.equal(requireTitle("Study"), "Study");
});
```

## Exercise 3

```typescript
test("async outcomes", async () => {
  await assert.doesNotReject(() => Promise.resolve("ready"));
  await assert.rejects(() => Promise.reject(new Error("failed")), /failed/);
});
```

## Exercise 4

```typescript
function setStatus(status: "open" | "closed"): void {
  console.log(status);
}

setStatus("open");
// @ts-expect-error unsupported status must remain invalid
setStatus("paused");
```

Widening the parameter to string removes the expected type error, so the directive itself reports a problem. That reveals an accidental contract weakening.

## Exercises 5 and 6

The exact refactor varies. A sound order is clean check, passing tests, one code change, targeted check, targeted tests, then full verification. A sound upgrade plan adds official release notes, a focused dependency update, review of every new diagnostic, runtime tests, and inspection of output or declarations when relevant.
