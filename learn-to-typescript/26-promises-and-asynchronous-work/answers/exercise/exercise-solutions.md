# Module 26 Exercise Solutions

## Exercise 1

The output is `A`, `C`, then `B`. The fulfillment handler runs after the current synchronous statements.

## Exercise 2

```typescript
function delayValue<T>(value: T, milliseconds: number): Promise<T> {
  return new Promise((resolve) => {
    setTimeout(() => resolve(value), milliseconds);
  });
}
```

## Exercise 3

```typescript
const doubled = Promise.resolve(5).then((value) => value * 2);
const labeled = doubled.then((value) => `Result: ${value}`);
labeled.then((value) => console.log(value));
```

The types are `Promise<number>` then `Promise<string>`.

## Exercise 4

```typescript
function requireNonnegative(value: number): Promise<number> {
  return value < 0
    ? Promise.reject(new Error("Negative value"))
    : Promise.resolve(value);
}

requireNonnegative(-1).catch((error: unknown) => {
  if (error instanceof Error) {
    console.log(error.message);
  }
});
```

## Exercise 5

```typescript
Promise.resolve(3)
  .then((value) => {
    return value * 2;
  })
  .then((value) => console.log(value));
```

The block body needs an explicit return.
