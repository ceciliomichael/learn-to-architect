# Module 33: Precise Type Design

## Before you start

Complete Modules 01 to 32. You should understand inference, literal types, generics, assertions, and public declarations.

## What you will learn

- preserve literal information with `as const`
- check a value against a type with `satisfies`
- use assertions only at proven boundaries
- create validated branded identifiers
- recognize practical variance in callbacks and collections
- balance precision with usability

## Why this matters

A type should reject meaningful mistakes and remain comfortable to use. Maximum narrowness is not always best. Precision should support real operations rather than make ordinary values difficult to pass.

## 1. Const assertions

```typescript
const routes = {
  home: "/",
  settings: "/settings",
} as const;
```

The const assertion:

- prevents literal widening
- marks object properties readonly in the inferred type
- turns array literals into readonly tuples

```typescript
const directions = ["north", "south"] as const;
type Direction = (typeof directions)[number];
```

`Direction` is `"north" | "south"`.

`as const` is static. It does not call `Object.freeze` at runtime.

## 2. `satisfies` checks without replacing the useful inferred type

```typescript
type RouteName = "home" | "settings";

const routes = {
  home: "/",
  settings: "/settings",
} satisfies Record<RouteName, string>;
```

The operator checks that every required route exists and values are strings. Unlike a direct annotation, it generally preserves more information about the expression for later use.

Compare:

```typescript
const annotated: Record<RouteName, string> = {
  home: "/",
  settings: "/settings",
};
```

The annotation gives the variable exactly the declared broad record type. `satisfies` checks compatibility while retaining the expression's own inferred property structure.

## 3. Combine const and satisfies carefully

```typescript
const levels = {
  beginner: 1,
  advanced: 2,
} as const satisfies Record<string, number>;
```

The values stay literal and readonly while the record constraint is checked.

Do not add `as const` when callers need a mutable object. Precision that blocks intended updates is not useful.

## 4. Assertions require evidence

```typescript
const element = document.querySelector("#name") as HTMLInputElement;
```

This can be wrong when no element exists or the element is another kind. A safer check is:

```typescript
const element = document.querySelector("#name");

if (element instanceof HTMLInputElement) {
  console.log(element.value);
}
```

Use an assertion only when a runtime invariant is established elsewhere and cannot be expressed to TypeScript. Keep it close to that evidence.

Avoid double assertions such as `value as unknown as Target`; they can force unrelated types together without proof.

## 5. Branded identifiers

Two ids may both be strings but should not be mixed:

```typescript
declare const userIdBrand: unique symbol;
declare const orderIdBrand: unique symbol;

type UserId = string & { readonly [userIdBrand]: true };
type OrderId = string & { readonly [orderIdBrand]: true };
```

Create branded values only at a validating boundary:

```typescript
function parseUserId(value: string): UserId | undefined {
  if (!value.startsWith("user_")) {
    return undefined;
  }

  return value as UserId;
}
```

The assertion is justified by the runtime format check. The brand has no runtime field and is not a security feature.

Brand only when mixing same-shaped values is a meaningful risk. Ordinary aliases are easier for many applications.

## 6. Practical variance in callbacks

Consider:

```typescript
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

type AnimalHandler = (animal: Animal) => void;
```

A function that only accepts Dog is not a safe general Animal handler. The caller may provide another Animal. Under strict function checking, TypeScript rejects unsafe parameter narrowing in relevant function positions.

A handler accepting a broader type can safely handle a narrower value. Think from the caller's permission: what values may it legally send?

## 7. Readonly improves safe sharing

A function that only reads should accept `readonly Animal[]`. This avoids requesting mutation permission and makes more inputs compatible.

Mutation makes type relationships harder because both reading and writing must remain safe. Public APIs should request only the permissions they need.

## 8. Design from use cases

Before adding an advanced type, list:

- valid calls that should work
- invalid calls that should fail
- runtime checks that still exist
- error messages a caller will see
- how often the type will change

A direct union, small interface, or overload is often better than a deep conditional type. Good type design reduces mistakes without becoming the hardest part of the program.

## Common mistakes

### Treating `as const` as runtime freezing

It changes inference only.

### Using `satisfies` as conversion

It checks compatibility and does not transform runtime data.

### Branding values without a validating constructor

Then callers rely on unsafe assertions scattered through the code.

### Making public types more precise than runtime behavior

The declaration must remain honest about missing and invalid data.

## Check your understanding

1. What three inference changes can `as const` make?
2. How does `satisfies` differ from a direct annotation?
3. Does a brand exist as runtime security data?
4. Why can a Dog-only callback not handle every Animal call?
5. What should decide whether an advanced type is worthwhile?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 34](../34-testing-and-maintaining-typescript/README.md) protects runtime behavior and type contracts while code changes.
