# Module 29: Advanced Function APIs

## Before you start

Complete Modules 01 to 28. You should understand function types, generics, unions, tuples, and narrowing.

## What you will learn

- accept a variable number of arguments with rest parameters
- spread arrays into calls safely
- write overload signatures
- choose a union instead of unnecessary overloads
- describe a function's `this` requirement
- connect callback input and output with generics

## Why this matters

Some functions have more than one useful call shape. TypeScript can describe those shapes, but a clear union or options object is often simpler than a clever overload list.

## 1. Rest parameters collect arguments

```typescript
function sum(...values: number[]): number {
  let total = 0;

  for (const value of values) {
    total = total + value;
  }

  return total;
}

console.log(sum(1, 2, 3));
```

The rest parameter must be last. Inside the function, it is an array.

Tuple rest types can describe a fixed remaining shape:

```typescript
function formatEntry(...entry: [name: string, score: number]): string {
  const [name, score] = entry;
  return `${name}: ${score}`;
}
```

## 2. Spread arguments into a call

```typescript
const numbers: [number, number] = [3, 4];
const result = Math.max(...numbers);
```

For a function requiring fixed positions, a tuple proves the argument count and types. An ordinary `number[]` may have too few or too many values for a fixed custom signature.

## 3. Overload signatures

```typescript
function formatValue(value: string): string;
function formatValue(value: number): string;
function formatValue(value: string | number): string {
  if (typeof value === "string") {
    return value.trim();
  }

  return value.toFixed(2);
}
```

The first signatures are visible call shapes. The final signature and body are the implementation. The implementation must handle every overload, but its signature is not an extra public call shape.

Use overloads when call inputs lead to meaningfully different, connected return types.

## 4. Prefer a union when the result is the same

The previous overloads are not needed because both calls return string:

```typescript
function formatValue(value: string | number): string {
  return typeof value === "string" ? value.trim() : value.toFixed(2);
}
```

A union is easier to maintain and accepts a variable already typed `string | number`. Overloads often reject a union argument because no single overload matches it.

## 5. Useful overload relationship

```typescript
function firstValue(value: string): string;
function firstValue<T>(value: readonly T[]): T | undefined;
function firstValue<T>(value: string | readonly T[]): string | T | undefined {
  return value[0];
}
```

The call shape connects string input to string output and array input to its item output. This relationship is a better reason for overloads.

## 6. A `this` parameter

```typescript
interface User {
  name: string;
}

function greet(this: User, message: string): string {
  return `${message}, ${this.name}`;
}

const user = { name: "Ana", greet };
console.log(user.greet("Hello"));
```

The fake first parameter describes the required calling context. It is erased and is not a runtime argument.

Arrow functions capture `this` from their surrounding scope and cannot declare a `this` parameter. Use this feature only for APIs that genuinely depend on method-style calls.

## 7. Generic callback relationships

```typescript
function mapValues<Input, Output>(
  values: readonly Input[],
  transform: (value: Input) => Output,
): Output[] {
  const results: Output[] = [];

  for (const value of values) {
    results.push(transform(value));
  }

  return results;
}
```

Input comes from the array. Output comes from the callback. The result connects to the callback output.

## 8. Consider an options object

When a function has many optional positional arguments, an object is clearer:

```typescript
interface SearchOptions {
  query: string;
  limit?: number;
  caseSensitive?: boolean;
}

function search(options: SearchOptions): string[] {
  return [];
}
```

Named properties are easier to read than several booleans or undefined placeholders.

## Common mistakes

### Writing overloads when a union is enough

Start with the simplest accurate signature.

### Exposing only the implementation signature

Callers see overload signatures, not arbitrary implementation-only combinations.

### Putting a rest parameter before another parameter

It must be last.

### Using positional booleans

An options object usually explains the call better.

## Check your understanding

1. What does a rest parameter contain inside the function?
2. Why can a tuple be important when spreading into fixed parameters?
3. When is a union simpler than overloads?
4. Is a `this` parameter passed at runtime?
5. What relationship does `mapValues` preserve?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 30](../30-conditional-types-and-infer/README.md) selects type results based on type relationships.
