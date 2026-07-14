# Module 23: Keys and Indexed Access Types

## Before you start

Complete Modules 01 to 22. You should understand generics, object types, and safe indexed access.

## What you will learn

- create a union of property names with `keyof`
- look up a property type with indexed access syntax
- capture the type of an existing value with type-position `typeof`
- connect an object, a valid key, and its result type
- understand common key limitations

## Why this matters

A helper that reads an object property should accept only real keys and return the type belonging to that exact key. These operators derive the relationship from the source shape instead of repeating it.

## 1. `keyof` creates a key union

```typescript
interface User {
  id: string;
  name: string;
  age: number;
}

type UserKey = keyof User;
```

`UserKey` is `"id" | "name" | "age"`.

```typescript
let key: UserKey = "name";

// Intentional error: not a User property.
key = "email";
```

## 2. Indexed access types

Use a property name in square brackets in a type position:

```typescript
type UserName = User["name"];
type UserAge = User["age"];
```

`UserName` is string. `UserAge` is number.

A union of keys produces a union of their value types:

```typescript
type UserText = User["id" | "name"];
```

`UserText` is string.

Use an existing key type:

```typescript
type UserValue = User[keyof User];
```

This becomes `string | number` for the current interface.

## 3. `typeof` in a type position

Runtime `typeof value` produces a string such as `"number"`.

Type-position `typeof` captures a static type:

```typescript
const defaultSettings = {
  theme: "light",
  pageSize: 20,
};

type Settings = typeof defaultSettings;
```

`Settings` has `theme: string` and `pageSize: number` because the object properties are mutable and their primitive values are widened.

The two uses of `typeof` have different contexts:

```typescript
console.log(typeof defaultSettings); // runtime expression
type Settings = typeof defaultSettings; // type expression
```

## 4. A type-safe property getter

```typescript
function getProperty<T, K extends keyof T>(object: T, key: K): T[K] {
  return object[key];
}
```

Read the relationships:

- `T` is the object type.
- `K` must be one of the keys of `T`.
- `T[K]` is the value type for that key.

```typescript
const user: User = { id: "u1", name: "Ana", age: 24 };

const name = getProperty(user, "name");
const age = getProperty(user, "age");
```

`name` is string and `age` is number.

## 5. Why `Object.keys` is broader

At runtime, `Object.keys(value)` returns strings. Objects can gain properties through wider references or runtime behavior, so TypeScript does not generally promise that every returned string is exactly `keyof T`.

Do not add a broad assertion automatically. When you own and validate a fixed object, a carefully scoped helper may be appropriate. Otherwise, narrow the runtime key before indexing.

## 6. Index signatures affect `keyof`

```typescript
interface NumberLookup {
  [key: string]: number;
}

type LookupKey = keyof NumberLookup;
```

The key type includes `string | number` because JavaScript object numeric keys are converted to strings. This is a language detail worth checking when generic key code meets dictionaries.

## 7. Derive, but keep a clear source of truth

Deriving `Settings` from a default value is useful when the value is the source of truth. Writing an interface separately is useful when the public contract should remain stable even if a particular default value changes.

Choose which direction represents the real design. Do not create circular layers of types only to avoid writing a simple shape.

## Common mistakes

### Writing `key: string` for a known object getter

Not every string is a valid key. Connect it with `K extends keyof T`.

### Confusing runtime and type-position `typeof`

One produces a runtime category string. The other captures a static type.

### Indexing with a key that was not proven

Runtime strings may not be real properties.

### Deriving types without deciding the source of truth

Use derivation when the value should control the type, not as a reflex.

## Check your understanding

1. What does `keyof User` produce?
2. What does `User["age"]` produce?
3. How does type-position `typeof` differ from runtime `typeof`?
4. What does `K extends keyof T` guarantee?
5. Why is `Object.keys` not simply typed as `(keyof T)[]` for every object?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 24](../24-utility-and-mapped-types/README.md) transforms complete object shapes into useful related shapes.
