# Module 22 Exercise Solutions

## Exercise 1

```typescript
function last<T>(values: readonly T[]): T | undefined {
  return values[values.length - 1];
}

console.log(last(["a", "b"]));
console.log(last([1, 2]));
console.log(last<string>([]));
```

## Exercise 2

```typescript
type Result<T> =
  | { ok: true; value: T }
  | { ok: false; error: string };

function requireText(value: string): Result<string> {
  return value.length > 0
    ? { ok: true, value }
    : { ok: false, error: "Text is required" };
}

function requirePositive(value: number): Result<number> {
  return value > 0
    ? { ok: true, value }
    : { ok: false, error: "Positive number required" };
}
```

## Exercise 3

```typescript
type Pair<First, Second> = [first: First, second: Second];

function makePair<First, Second>(first: First, second: Second): Pair<First, Second> {
  return [first, second];
}

const pair = makePair("age", 24);
```

The tuple type is `[string, number]`.

## Exercise 4

```typescript
function describeId<T extends { id: string }>(value: T): string {
  return `ID: ${value.id}`;
}

const user = { id: "u1", name: "Ana" };
console.log(describeId(user));
console.log(user.name);
```

The constraint requires an id without discarding the more specific user shape.

## Exercise 5

```typescript
function logAnything(value: unknown): void {
  console.log(value);
}
```

The type appears only once and does not affect an output or another parameter. No relationship needs preservation.
