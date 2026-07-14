# Module 16: Tuples and Readonly Collections

## Before you start

Complete Modules 01 to 15. You should understand arrays, object types, optional values, and readonly properties.

## What you will learn

- describe fixed array positions with a tuple
- use labels to document tuple positions
- destructure arrays and objects
- accept collections without permission to change them
- choose between a tuple, array, and object

## Why this matters

An ordinary array can grow and every position has the same item type. Some data has a small fixed order, such as a coordinate pair. A tuple can describe that order. Readonly collection types can also state that a function only reads its input.

## 1. A tuple has fixed positions

```typescript
type Coordinate = [number, number];

const point: Coordinate = [10, 20];
```

Index 0 and index 1 are numbers, and the tuple expects exactly two required positions.

This is invalid:

```typescript
// Intentional error: the second position must be a number.
const invalidPoint: Coordinate = [10, "twenty"];
```

Tuples can have different types by position:

```typescript
type Entry = [string, number];
const scoreEntry: Entry = ["Ana", 90];
```

## 2. Tuple labels improve reading

```typescript
type Coordinate = [x: number, y: number];
```

The labels help editor hints. They do not create runtime properties. You still read `point[0]`, not `point.x`.

If named access would be clearer, use an object:

```typescript
interface CoordinateObject {
  x: number;
  y: number;
}
```

## 3. Destructure a tuple

Destructuring assigns positions to names:

```typescript
type Coordinate = [x: number, y: number];
const point: Coordinate = [10, 20];
const [x, y] = point;

console.log(x);
console.log(y);
```

This often makes tuple positions easier to use.

Objects have matching destructuring:

```typescript
const book = { title: "Dune", pages: 412 };
const { title, pages } = book;
```

Array destructuring follows position. Object destructuring follows property names.

## 4. Optional tuple positions

```typescript
type Range = [start: number, end?: number];

const openRange: Range = [10];
const closedRange: Range = [10, 20];
```

Optional positions must come after required positions. Reading `openRange[1]` can produce undefined.

Use optional tuple members only when position remains easy to understand. An object is often clearer when many fields are optional.

## 5. Readonly arrays

```typescript
function printNames(names: readonly string[]): void {
  for (const name of names) {
    console.log(name);
  }

  // Intentional error: the parameter does not permit mutation.
  names.push("New name");
}
```

`readonly string[]` says this function may read the array but may not use mutating methods through this parameter.

Another spelling is `ReadonlyArray<string>`. They describe the same kind of readonly view.

## 6. Accept readonly inputs when you only read

```typescript
function sum(values: readonly number[]): number {
  let total = 0;

  for (const value of values) {
    total = total + value;
  }

  return total;
}
```

This function accepts both ordinary number arrays and readonly number arrays because it promises not to change either.

A function requiring `number[]` cannot safely receive a readonly array because it might call `push`.

## 7. Readonly tuples

```typescript
type Coordinate = readonly [x: number, y: number];

const point: Coordinate = [10, 20];

// Intentional error: position 0 is readonly.
point[0] = 30;
```

Like readonly object properties, this is a static restriction. It does not automatically freeze the runtime array.

## 8. Choose the clearest structure

Use an array when:

- the list may have any length
- items share one type
- iteration is the main use

Use a tuple when:

- the number and order of positions are part of the meaning
- the tuple stays short
- each position is easy to remember or destructure

Use an object when:

- named properties explain the data better
- there are several optional fields
- fields are often accessed individually

## Common mistakes

### Using a tuple for a long record

An object is easier to read than remembering what index 7 means.

### Believing tuple labels create properties

They are type documentation only.

### Requiring mutable arrays for read-only work

Use a readonly parameter to accept more callers and protect intent.

### Treating readonly as runtime freezing

It blocks writes through the static type, not every possible runtime mutation.

## Check your understanding

1. How does a tuple differ from an ordinary array?
2. Do tuple labels exist at runtime?
3. What does destructuring do?
4. Why can a readonly array parameter accept a mutable array?
5. When is an object clearer than a tuple?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 17](../17-function-types-and-callbacks/README.md) describes functions as values and builds clearer callback contracts.
