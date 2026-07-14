# Module 11 Exercise Solutions

## Exercise 1

- `course` is inferred. Its variable can have the literal type `"TypeScript"` because it is a primitive `const`.
- `lesson` is explicitly annotated as `number`.
- `complete` is inferred, with the literal type `false` for this primitive `const`.
- `scores` is explicitly annotated as `number[]`.

Editor displays can simplify or expand these types depending on context, but the key distinction is whether the source contains an annotation.

## Exercise 2

```typescript
const title = "Morning Plan";
const minutes = 25;
const isComplete = false;
const labels = ["study", "focus"];
```

The values make all four types clear. If the final array were empty, `const labels: string[] = [];` would clearly state which items it is meant to receive.

## Exercise 3

```typescript
function calculateRectangleArea(width: number, height: number): number {
  return width * height;
}

console.log(calculateRectangleArea(5, 4));
```

The output is `20`. Returning a template string would break the written `number` promise, so TypeScript reports the mismatch at the function implementation.

## Exercise 4

```typescript
const values = [2, 4, 6];
const doubled = values.map((value) => value * 2);

console.log(doubled);
```

TypeScript infers `value` as `number` from the array and the `map` callback context. It infers `doubled` as `number[]`.

## Exercise 5

The emitted JavaScript is similar to:

```javascript
function describeCount(count) {
  return `Count: ${count}`;
}

console.log(describeCount(3));
```

The parameter annotation `: number` and return annotation `: string` were removed. The executable function, return statement, template string, and call remain.
