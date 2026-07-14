# Module 15: Optional and Readonly Data

## Before you start

Complete Modules 01 to 14. You should understand object types, missing values, and narrowing.

## What you will learn

- model an object property that may be absent
- distinguish absence from a present `undefined` value
- read optional data with checks, optional chaining, and nullish coalescing
- prevent assignment through a type with `readonly`
- describe a dictionary with an index signature

## Why this matters

Not every object has every piece of information. A profile may have no nickname. A lookup may not contain a requested key. Accurate types make these cases visible instead of waiting for a runtime failure.

## 1. Optional properties

Add `?` after a property name when the property itself may be absent:

```typescript
interface Profile {
  name: string;
  nickname?: string;
}

const first: Profile = { name: "Ana" };
const second: Profile = { name: "Ben", nickname: "B" };
```

When you read an optional property, its value may be `undefined`:

```typescript
function printNickname(profile: Profile): void {
  if (profile.nickname !== undefined) {
    console.log(profile.nickname.toUpperCase());
  }
}
```

## 2. Optional is different from required with `undefined`

Compare these shapes:

```typescript
interface OptionalNote {
  note?: string;
}

interface PresentNote {
  note: string | undefined;
}
```

This value satisfies `OptionalNote`:

```typescript
const optional: OptionalNote = {};
```

This value does not satisfy `PresentNote` because the key is required:

```typescript
// Intentional error: note must be present.
const present: PresentNote = {};
```

A valid `PresentNote` can be `{ note: undefined }`.

With `exactOptionalPropertyTypes` enabled, `note?: string` means the property is absent or contains a string. Explicitly assigning `undefined` requires including `undefined` in the property value type. Module 19 enables this option.

## 3. Optional chaining

Optional chaining stops property access when the value to its left is `null` or `undefined`:

```typescript
interface Account {
  displayName?: string;
}

function getNameLength(account: Account): number | undefined {
  return account.displayName?.length;
}
```

If the name exists, the function returns its length. Otherwise it returns `undefined`.

Optional chaining does not treat an empty string or zero as missing.

## 4. Nullish coalescing

Use `??` to provide a fallback for `null` or `undefined`:

```typescript
function displayNickname(profile: Profile): string {
  return profile.nickname ?? "No nickname";
}
```

Compare `??` with `||`:

```typescript
const savedVolume = 0;

console.log(savedVolume ?? 5);
console.log(savedVolume || 5);
```

The first prints `0` because zero is present. The second prints `5` because `||` treats zero as false-like.

Use `??` when only null or undefined should trigger the fallback.

## 5. Readonly properties

```typescript
interface User {
  readonly id: string;
  name: string;
}

const user: User = {
  id: "user-1",
  name: "Ana",
};

user.name = "Anabel";

// Intentional error: id is readonly through User.
user.id = "user-2";
```

`readonly` is a static restriction on assignment through that type. It does not freeze the object at runtime.

It is also shallow:

```typescript
interface Settings {
  readonly theme: {
    name: string;
  };
}

const settings: Settings = { theme: { name: "light" } };
settings.theme.name = "dark";
```

The `theme` property cannot be assigned a different object, but the nested object's own `name` property is still writable.

## 6. Index signatures for dictionaries

Sometimes an object has string keys not known in advance:

```typescript
interface ScoreLookup {
  [learnerName: string]: number;
}

const scores: ScoreLookup = {
  Ana: 90,
  Ben: 84,
};

scores.Cy = 88;
```

The parameter name `learnerName` is documentation. It means any string key has a number value.

An indexed lookup may be missing at runtime:

```typescript
const score = scores["Unknown"];
```

With `noUncheckedIndexedAccess`, this has type `number | undefined`. That accurately reflects the possible missing key.

## 7. Known properties must fit the index signature

```typescript
interface Inventory {
  [itemName: string]: number;
  pencil: number;
}
```

The known `pencil` property fits because it is a number.

This would conflict:

```typescript
interface InvalidInventory {
  [itemName: string]: number;
  // Intentional error: a known string property conflicts.
  label: string;
}
```

Use an index signature only when arbitrary keys genuinely share one value type.

## Common mistakes

### Using optional to mean every kind of uncertainty

Use it when the property may be absent. A required but possibly undefined property is different.

### Using `||` when zero or empty text is valid

Use `??` for a null-or-undefined fallback.

### Believing `readonly` freezes runtime data deeply

It is a compile-time, shallow assignment rule unless nested properties are also readonly and runtime freezing is handled separately.

### Assuming dictionary lookup always finds a value

Check for `undefined`, especially with strict indexed access.

## Check your understanding

1. What does `nickname?: string` allow?
2. How does it differ from `nickname: string | undefined`?
3. When does `??` use its right side?
4. Does `readonly` freeze an object at runtime?
5. Why can a dictionary lookup return `undefined`?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 16](../16-tuples-and-readonly-collections/README.md) models fixed positions and collections that should not be changed through a type.
