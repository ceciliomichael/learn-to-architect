# Module 22: Generics

## Before you start

Complete Modules 01 to 21. You should understand function contracts, aliases, interfaces, arrays, and result unions.

## What you will learn

- preserve relationships between types with a type parameter
- let TypeScript infer generic arguments
- write generic functions, aliases, and interfaces
- add a constraint when an operation requires a property
- use more than one type parameter when relationships require it
- avoid a generic when one concrete type is clearer

## Why this matters

Some code works the same way for many types while preserving the exact type it receives. A generic expresses that relationship without replacing useful information with `unknown` or a broad union.

## 1. The relationship problem

This function loses information:

```typescript
function firstUnknown(values: readonly unknown[]): unknown {
  return values[0];
}
```

When a string array goes in, the caller still receives unknown.

A generic preserves the item type:

```typescript
function first<T>(values: readonly T[]): T | undefined {
  return values[0];
}
```

`T` is a type parameter. For a string array, `T` becomes string. For a number array, it becomes number.

## 2. Generic inference

```typescript
const firstName = first(["Ana", "Bo"]);
const firstScore = first([90, 84]);
```

TypeScript infers:

- `firstName` is `string | undefined`
- `firstScore` is `number | undefined`

You can provide a type argument explicitly:

```typescript
const emptyFirst = first<string>([]);
```

Inference is usually preferable when the input already makes the type clear.

## 3. Generic identity

```typescript
function identity<T>(value: T): T {
  return value;
}
```

The important idea is not that `T` means any type. It means the same chosen type appears in the input and output.

Compare a union:

```typescript
function looseIdentity(value: string | number): string | number {
  return value;
}
```

Calling the union version with a string still gives a union result. Calling the generic version preserves string.

## 4. Generic type aliases

Make the result pattern reusable:

```typescript
type Result<T> =
  | { ok: true; value: T }
  | { ok: false; error: string };

function parseCount(text: string): Result<number> {
  const value = Number(text);

  if (!Number.isInteger(value)) {
    return { ok: false, error: "Expected a whole number" };
  }

  return { ok: true, value };
}
```

`Result<string>` and `Result<number>` share the same success-or-failure structure while keeping different success values.

## 5. More than one type parameter

```typescript
type Pair<Left, Right> = {
  left: Left;
  right: Right;
};

const entry: Pair<string, number> = {
  left: "score",
  right: 90,
};
```

Use descriptive type parameter names when single letters would be unclear.

## 6. Generic interfaces

```typescript
interface Container<T> {
  value: T;
  updatedAt: Date;
}

const message: Container<string> = {
  value: "Saved",
  updatedAt: new Date(),
};
```

The interface structure is reusable while `value` stays precise.

## 7. Constraints

An unconstrained `T` has no known properties:

```typescript
function getLength<T>(value: T): number {
  // Intentional error: not every T has length.
  return value.length;
}
```

Require the capability:

```typescript
interface HasLength {
  length: number;
}

function getLength<T extends HasLength>(value: T): number {
  return value.length;
}
```

Strings, arrays, and other values with a numeric length can be passed. The generic still preserves their more specific type where needed.

## 8. Return the same object type

```typescript
interface HasId {
  id: string;
}

function logId<T extends HasId>(value: T): T {
  console.log(value.id);
  return value;
}
```

The constraint permits access to `id`. Returning `T` preserves any additional properties the caller provided.

## 9. Do not add a generic without a relationship

This generic adds no value:

```typescript
function printValue<T>(value: T): void {
  console.log(value);
}
```

If the function only prints and does not connect `T` to another position, `unknown` is often clearer:

```typescript
function printValue(value: unknown): void {
  console.log(value);
}
```

A useful generic type parameter usually appears more than once or controls part of the returned structure.

## Common mistakes

### Reading `T` as one global type

Each call or constructed generic type chooses its own type argument.

### Using `any` instead of preserving a relationship

`any` loses checks. A generic can keep the exact connection.

### Accessing properties on unconstrained `T`

Add the smallest honest constraint.

### Adding many type parameters too early

Use only the relationships the API needs.

## Check your understanding

1. What relationship does `identity<T>(value: T): T` express?
2. Why does `first` return `T | undefined`?
3. When can TypeScript infer a type argument?
4. What does `extends HasLength` mean in a generic parameter?
5. When might `unknown` be clearer than a generic?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 23](../23-keys-and-indexed-access-types/README.md) connects generic values to valid object keys and property types.
