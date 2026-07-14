# Module 29 Exercise Solutions

## Exercise 1

```typescript
function joinWith(separator: string, ...values: string[]): string {
  return values.join(separator);
}
```

## Exercise 2

```typescript
function createRange(start: number, end: number): number[] {
  const values: number[] = [];
  for (let value = start; value <= end; value += 1) values.push(value);
  return values;
}

const rangeArguments: [number, number] = [2, 5];
console.log(createRange(...rangeArguments));
```

## Exercise 3

```typescript
function toText(value: string | number): string {
  return String(value);
}
```

Both inputs produce the same return type, so a union is direct and accepts union-typed variables.

## Exercise 4

```typescript
function double(value: number): number;
function double(value: string): string;
function double(value: string | number): string | number {
  return typeof value === "number" ? value * 2 : value.repeat(2);
}
```

## Exercise 5

```typescript
function mapValues<Input, Output>(values: readonly Input[], transform: (value: Input) => Output): Output[] {
  const results: Output[] = [];
  for (const value of values) results.push(transform(value));
  return results;
}

const labels = mapValues([1, 2], (value) => `Item ${value}`);
```
