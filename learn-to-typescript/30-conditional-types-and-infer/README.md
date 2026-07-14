# Module 30: Conditional Types and Infer

## Before you start

Complete Modules 01 to 29. You should understand generics, unions, indexed access, and function types.

## What you will learn

- select a type with `T extends U ? X : Y`
- understand distributive conditional types
- prevent distribution when needed
- capture a type part with `infer`
- read small helpers built from conditional types
- stop when a direct type is clearer

## Why this matters

Library types sometimes need to calculate a result from another type. Conditional types are useful for these relationships, but they can make ordinary application code harder to read. Learn to recognize them and use small focused versions.

## 1. Conditional type syntax

```typescript
type IsString<T> = T extends string ? true : false;

type A = IsString<string>; // true
type B = IsString<number>; // false
```

Read it as: if T is assignable to string, choose true; otherwise choose false.

The result is a static type. No runtime condition is emitted.

## 2. Choose a useful result

```typescript
type LabelFor<T> = T extends number ? { numericLabel: string } : { textLabel: string };
```

Conditional types are strongest when callers and results already have a real type-level relationship. They should not replace ordinary runtime decisions.

## 3. Distribution over unions

When a conditional checks a bare type parameter, it distributes over union members:

```typescript
type ToArray<T> = T extends unknown ? T[] : never;
type Result = ToArray<string | number>;
```

`Result` is `string[] | number[]`, not `(string | number)[]`.

Think of TypeScript applying the conditional to each member and joining the results.

## 4. Prevent distribution

Wrap both sides in one-element tuples:

```typescript
type ToArrayTogether<T> = [T] extends [unknown] ? T[] : never;
type Result = ToArrayTogether<string | number>;
```

Now `Result` is `(string | number)[]`.

Use this only when union-as-a-whole behavior is the real intention.

## 5. Filter union members

```typescript
type KeepStrings<T> = T extends string ? T : never;
type TextOnly = KeepStrings<string | number | boolean>;
```

Distribution produces `string | never | never`, which simplifies to string.

This idea powers utilities such as `Exclude` and `Extract`.

## 6. Infer an array item type

```typescript
type ElementOf<T> = T extends readonly (infer Item)[] ? Item : never;

type Name = ElementOf<string[]>;
type Score = ElementOf<readonly number[]>;
```

`infer Item` asks TypeScript to capture the array member type in the true branch.

## 7. Infer a Promise result

```typescript
type PromiseValue<T> = T extends Promise<infer Value> ? Value : T;

type A = PromiseValue<Promise<string>>; // string
type B = PromiseValue<number>; // number
```

The built-in `Awaited<T>` handles nested Promises and Promise-like values more completely. Prefer the built-in utility in real code when it matches the need.

## 8. Infer a function return

```typescript
type FunctionResult<T> = T extends (...arguments_: never[]) => infer Return
  ? Return
  : never;

type Result = FunctionResult<() => number>;
```

The built-in `ReturnType<T>` is the normal choice. Writing a small version helps explain how `infer` works.

## 9. Keep conditions shallow

This is readable:

```typescript
type IdOf<T> = T extends { id: infer Id } ? Id : never;
```

Several nested conditional types can produce difficult errors and slow understanding. Name intermediate steps, prefer built-ins, and consider an explicit type when the relationship is not central.

## Common mistakes

### Expecting a runtime branch

Conditional types exist only during checking.

### Being surprised by union distribution

A bare type parameter distributes. Use tuple wrapping when treating the union as one value.

### Reimplementing built-in utilities

Use `Awaited`, `ReturnType`, `Exclude`, and other built-ins when appropriate.

### Using conditional types as a skill display

Clarity is the goal. Advanced syntax is not automatically better design.

## Check your understanding

1. How do you read `T extends U ? X : Y`?
2. What happens to a bare generic conditional over a union?
3. How can distribution be prevented?
4. What does `infer` capture?
5. When should you prefer a built-in utility?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 31](../31-advanced-mapped-and-template-literal-types/README.md) transforms property names and derives string patterns.
