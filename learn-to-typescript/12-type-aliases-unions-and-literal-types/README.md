# Module 12: Type Aliases, Unions, and Literal Types

## Before you start

Complete Modules 01 to 11. You should understand inference and annotations.

## What you will learn

- give a type expression a reusable name
- allow one of several types with a union
- limit values with literal types
- model `null` and `undefined` honestly
- understand that aliases do not create runtime values

## Why this matters

Primitive types can be too broad. A status is not just any string. It may be exactly `"idle"`, `"loading"`, or `"done"`. Precise types make valid choices visible and catch impossible assignments.

## 1. A type alias names a type

```typescript
type UserId = string;

const currentUserId: UserId = "user-104";
```

`type` creates an alias. It gives a type expression a name that can be reused.

Aliases use Pascal case by convention: `UserId`, `TaskStatus`, and `SearchResult`.

This simple alias improves meaning, but it does not create a distinct kind of string. Any string can still be assigned to `UserId`.

## 2. Union types allow alternatives

```typescript
type Identifier = string | number;

let id: Identifier = "A-10";
id = 10;
```

The vertical bar means or. `Identifier` permits a string or a number.

This does not permit unrelated values:

```typescript
// Intentional error: boolean is not part of the union.
id = true;
```

When a value has a union type, TypeScript only allows operations safe for every member until the code checks which member is present. Module 13 teaches those checks.

## 3. Literal types represent exact values

```typescript
type Direction = "north" | "south" | "east" | "west";

let direction: Direction = "north";
direction = "east";

// Intentional error: this exact string is not allowed.
direction = "up";
```

Each quoted type is a string literal type. It represents one exact value rather than all strings.

Literal unions work well for a fixed set of choices:

```typescript
type Theme = "light" | "dark";
type Rating = 1 | 2 | 3 | 4 | 5;
type Enabled = true | false;
```

The last alias is usually unnecessary because it is the same possible values as `boolean`, but it shows that boolean literal types exist.

## 4. Literal types improve function inputs

```typescript
type TextAlignment = "left" | "center" | "right";

function setAlignment(alignment: TextAlignment): void {
  console.log(`Alignment: ${alignment}`);
}

setAlignment("center");

// Intentional error: not an accepted choice.
setAlignment("middle");
```

The `void` return type means the function does not return a useful value to its caller.

Editors can suggest the allowed strings, and misspellings become type errors.

## 5. `null` and `undefined`

JavaScript has two common missing-value values:

- `undefined` often means no value was provided or found.
- `null` is often used deliberately to mean no value.

Under strict null checking, neither is automatically accepted where a string is required:

```typescript
let selectedName: string = "Ana";

// Intentional errors under strict null checking.
selectedName = undefined;
selectedName = null;
```

Include a missing value when it is part of the real model:

```typescript
let selectedName: string | null = null;
selectedName = "Ana";
```

Do not add `null` or `undefined` to every type. Add them only when absence is possible and meaningful.

## 6. A function can return a union

```typescript
function findLabel(code: number): string | undefined {
  if (code === 1) {
    return "one";
  }

  if (code === 2) {
    return "two";
  }

  return undefined;
}
```

The return type tells callers that a label might not exist. Callers must check before using string-only methods.

## 7. Aliases disappear at runtime

```typescript
type Status = "idle" | "working";
const status: Status = "idle";
```

The emitted JavaScript contains the value and variable, but not the `Status` alias. You cannot print or compare against the type name at runtime.

This is invalid:

```typescript
// Intentional error: Status is a type, not a runtime value.
console.log(Status);
```

## 8. Do not use a union to hide unclear data

This type accepts too many unrelated meanings:

```typescript
type Data = string | number | boolean | null;
```

A union is useful when each member is an honest possibility for the same concept. Prefer a smaller type with a clear name.

## Common mistakes

### Expecting an alias to create a distinct runtime value

It only names a static type.

### Using `string` for a fixed set of choices

A literal union catches misspellings and shows valid choices.

### Adding `undefined` to avoid fixing a missing case

The union should describe reality, and code should still handle the missing branch.

### Calling a member-specific method on a union

Check the current value first. That is narrowing, taught next.

## Check your understanding

1. What does the `|` symbol mean in a type?
2. How is `"open"` different from `string` in a type position?
3. Does `type UserId = string` prevent an ordinary string from being assigned?
4. When should a type include `null` or `undefined`?
5. Can a type alias be printed at runtime?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 13](../13-narrowing/README.md) teaches how checks make a union value safe to use.
