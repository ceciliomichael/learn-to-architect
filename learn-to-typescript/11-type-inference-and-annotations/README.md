# Module 11: Type Inference and Annotations

## Before you start

Complete Modules 01 to 10. You should be comfortable writing small programs with functions, arrays, and objects.

## What you will learn

- separate a value from its static type
- see how TypeScript infers types from code
- add annotations where they improve a contract
- understand widening and contextual typing at a practical level
- explain what happens to ordinary type annotations at runtime

## Why this matters

TypeScript can often understand a type without being told. Good TypeScript code lets inference handle obvious local details and writes types where a reader or caller needs a clear promise.

## 1. Values and types answer different questions

```typescript
const city = "Iloilo";
```

The value is the text `"Iloilo"`. The static type describes which values TypeScript permits in that place.

Static means TypeScript uses the information while checking code. Runtime means JavaScript is executing the program.

The type checker can reject a program before you run it, but a type annotation does not inspect live data by itself.

## 2. Type inference

Type inference means TypeScript works out a type from nearby code:

```typescript
const title = "A Short Book";
let page = 1;
const isOpen = true;
const tags = ["fiction", "short"];
```

You do not need to write these longer forms:

```typescript
const title: string = "A Short Book";
let page: number = 1;
const isOpen: boolean = true;
const tags: string[] = ["fiction", "short"];
```

Both versions check the same basic assignments. The first is quieter and still clear.

## 3. Annotations state an expected type

An annotation appears after the name:

```typescript
let score: number = 0;
```

Annotations are useful when the first value does not reveal enough:

```typescript
const names: string[] = [];
```

Without `string[]`, an empty array may not communicate the intended item type clearly across different contexts and compiler settings.

Annotations are also important on function parameters:

```typescript
function calculateTotal(price: number, quantity: number) {
  return price * quantity;
}
```

The caller now has a clear contract: both arguments must be numbers.

## 4. Return type inference

TypeScript reads return statements:

```typescript
function calculateTotal(price: number, quantity: number) {
  return price * quantity;
}
```

The inferred return type is `number`.

You may write it explicitly:

```typescript
function calculateTotal(price: number, quantity: number): number {
  return price * quantity;
}
```

An explicit return type can document a public function or prevent an accidental change to its contract. It is not required on every function.

This annotation catches a changed implementation:

```typescript
function calculateTotal(price: number, quantity: number): number {
  // Intentional error: a string does not match the promised number.
  return `${price * quantity}`;
}
```

## 5. `let` and `const` can infer differently

```typescript
let direction = "north";
const fixedDirection = "north";
```

`direction` needs to allow other strings because a `let` variable can be reassigned. The type is widened to `string`.

The `const` variable cannot be reassigned, so TypeScript can preserve the exact literal type `"north"` for the variable itself.

This detail becomes useful with literal types in Module 12.

## 6. Contextual typing

The surrounding code can supply a type:

```typescript
const names = ["Ana", "Bo"];

names.map((name) => name.toUpperCase());
```

The callback parameter has no written annotation. TypeScript knows that `map` will give it an item from a string array, so `name` is understood as a string.

This is contextual typing. It is why many callback parameters do not need repeated annotations.

## 7. Object inference

```typescript
const task = {
  title: "Study",
  minutes: 30,
  isComplete: false,
};
```

TypeScript infers each property type. It checks later updates:

```typescript
task.minutes = 45;

// Intentional error: minutes is a number property.
task.minutes = "forty-five";
```

When an object shape is reused as a function contract, give it a name. Module 14 covers aliases and interfaces for object shapes.

## 8. Annotations do not convert values

This is an error, not a conversion:

```typescript
// Intentional error: the value is still a string.
const amount: number = "50";
```

Writing `: number` does not turn text into a number. Conversion is runtime work and must be handled deliberately.

## 9. Ordinary type annotations are removed

TypeScript source:

```typescript
function greet(name: string): string {
  return `Hello, ${name}`;
}
```

Emitted JavaScript is similar to:

```javascript
function greet(name) {
  return `Hello, ${name}`;
}
```

The `: string` annotations are gone. JavaScript runtimes do not use ordinary TypeScript annotations.

This is why receiving network data does not become safe merely because your code writes a type. Module 20 teaches runtime validation.

## 10. A practical annotation rule

Start with these choices:

- Let obvious local values be inferred.
- Annotate function parameters.
- Consider annotating exported or important return types.
- Annotate empty collections when their intended item type is not otherwise clear.
- Name reused object shapes instead of repeating long inline types.

These are useful defaults, not laws.

## Common mistakes

### Annotating every local value

It adds noise without adding information when the value already makes the type obvious.

### Believing an annotation changes runtime data

It only tells the checker what should be allowed.

### Leaving function parameters unclear

With strict checking, parameters need a known type from an annotation or context.

### Fighting correct inference

If TypeScript reports a mismatch, first check whether the program is storing the wrong kind of value.

## Check your understanding

1. What is type inference?
2. When is an annotation useful for an empty array?
3. Why can a return annotation catch an implementation mistake?
4. What provides the type of `name` in `names.map((name) => name.toUpperCase())`?
5. Do ordinary type annotations remain in emitted JavaScript?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 12](../12-type-aliases-unions-and-literal-types/README.md) combines simple types into more precise choices.
