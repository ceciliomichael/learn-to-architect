# Module 16 Exercise Solutions

## Exercise 1

```typescript
type Coordinate = readonly [x: number, y: number];

const point: Coordinate = [10, 20];
const [x, y] = point;

console.log(x);
console.log(y);
```

## Exercise 2

```typescript
type NameAndLength = [name: string, length: number];

function describeText(text: string): NameAndLength {
  return [text, text.length];
}

console.log(describeText("TypeScript"));
```

The result is `["TypeScript", 10]`.

## Exercise 3

```typescript
function findMaximum(values: readonly number[]): number | undefined {
  const first = values[0];

  if (first === undefined) {
    return undefined;
  }

  let maximum = first;

  for (const value of values) {
    if (value > maximum) {
      maximum = value;
    }
  }

  return maximum;
}
```

The explicit first-item check handles empty input and gives the loop a real starting value.

## Exercise 4

- Use an array for a month of temperatures because the list length can vary and items share a type.
- A short coordinate tuple can work when the position order is established. An object is also reasonable when named access matters more.
- Use an object for the customer because names and optional fields improve clarity.
- Use a tuple for the short label-and-count pair when it is naturally handled together.

## Exercise 5

```typescript
function firstName(names: readonly string[]): string | undefined {
  return names[0];
}
```

The function promises only to read, so both mutable and readonly arrays can be passed.
