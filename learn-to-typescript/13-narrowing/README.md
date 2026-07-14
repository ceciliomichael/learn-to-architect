# Module 13: Narrowing

## Before you start

Complete Modules 01 to 12. You should understand decisions and union types.

## What you will learn

- understand why a union allows only shared operations
- narrow with `typeof`, equality, and `Array.isArray`
- remove missing cases with early returns
- use truthiness without losing valid values
- follow control-flow narrowing through branches

## Why this matters

A union says a value has several possibilities. Before using behavior that belongs to only one possibility, the program must check which value is present. TypeScript follows those checks.

## 1. A union keeps only universally safe operations

```typescript
function formatId(id: string | number): string {
  // Intentional error: numbers have no toUpperCase method.
  return id.toUpperCase();
}
```

The caller may pass a number. TypeScript blocks the string-only method until the code checks the value.

## 2. Narrow with `typeof`

```typescript
function formatId(id: string | number): string {
  if (typeof id === "string") {
    return id.toUpperCase();
  }

  return id.toFixed(0);
}
```

Inside the first branch, TypeScript narrows `id` to `string`. After that branch returns, the only remaining possibility is `number`.

`typeof` is useful for these primitive categories:

- `"string"`
- `"number"`
- `"boolean"`
- `"undefined"`
- `"function"`
- `"object"`
- `"bigint"`
- `"symbol"`

There is a historical JavaScript detail: `typeof null` is `"object"`. Check `null` directly.

## 3. Narrow with equality

```typescript
function printSelection(selection: string | null): void {
  if (selection === null) {
    console.log("Nothing selected");
    return;
  }

  console.log(selection.toUpperCase());
}
```

The early return handles the missing case. Code below it can treat `selection` as a string.

Checks with `!== undefined` work the same way for an undefined member.

## 4. Narrow arrays with `Array.isArray`

```typescript
function countInput(input: string | string[]): number {
  if (Array.isArray(input)) {
    return input.length;
  }

  return input.length;
}
```

Both branches use `length`, but its meaning differs. For an array, it is the number of items. For a string, it is the number of text units.

This example uses array-only behavior:

```typescript
function joinInput(input: string | string[]): string {
  if (Array.isArray(input)) {
    return input.join(", ");
  }

  return input;
}
```

## 5. Truthiness needs care

JavaScript conditions treat some values as false, including:

- `false`
- `0`
- an empty string
- `null`
- `undefined`
- `NaN`

This check may hide a valid empty string:

```typescript
function printText(text: string | undefined): void {
  if (text) {
    console.log(text);
  }
}
```

If an empty string is valid and should be printed, check only the missing case:

```typescript
if (text !== undefined) {
  console.log(text);
}
```

Use truthiness when all false-like values genuinely mean the same thing in your program.

## 6. Control flow carries type information

```typescript
function normalize(value: string | number | null): string {
  if (value === null) {
    return "";
  }

  if (typeof value === "number") {
    return value.toFixed(2);
  }

  return value.trim();
}
```

Each completed branch removes a member. The final branch has only `string` left.

## 7. Narrow object unions with a property check

The `in` operator checks whether a property exists at runtime:

```typescript
type EmailContact = { email: string };
type PhoneContact = { phone: string };

function printContact(contact: EmailContact | PhoneContact): void {
  if ("email" in contact) {
    console.log(contact.email);
  } else {
    console.log(contact.phone);
  }
}
```

Use this when the shapes naturally have different properties. Module 28 teaches a clearer pattern for state objects that share an explicit label.

## 8. Narrowing is runtime logic plus static understanding

The `if` statement runs in JavaScript. TypeScript studies that real runtime logic and adjusts its static understanding inside each path.

The check is not inserted automatically. Your source code must perform it.

## Common mistakes

### Using an assertion instead of a check

An assertion can silence the checker without proving anything at runtime. Real uncertainty needs a real check.

### Checking `typeof value === "object"` and forgetting `null`

Add `value !== null` before using object properties.

### Using truthiness when zero or empty text is valid

Check `null` or `undefined` directly.

### Repeating checks after an early return

Let control flow remove the handled member and keep the remaining code simple.

## Check your understanding

1. Why can a union value use only operations shared by all members?
2. What does `typeof null` return?
3. How does an early return help narrowing?
4. When is `Array.isArray` useful?
5. Why can a truthiness check accidentally ignore valid data?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 14](../14-object-types-and-interfaces/README.md) gives reusable names to structured object data.
