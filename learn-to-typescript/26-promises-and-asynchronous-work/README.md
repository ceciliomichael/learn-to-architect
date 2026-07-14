# Module 26: Promises and Asynchronous Work

## Before you start

Complete Modules 01 to 25. You should understand callbacks, generics, errors, and strict project settings.

## What you will learn

- distinguish immediate and delayed results
- understand pending, fulfilled, and rejected Promise states
- read `Promise<T>`
- handle completion with `then`, failure with `catch`, and cleanup with `finally`
- create a small Promise wrapper for a timer
- understand what asynchronous code does not guarantee

## Why this matters

Network requests, timers, and many file operations finish later. A Promise represents one future completion or failure and lets code attach the next steps.

## 1. Immediate versus delayed results

An ordinary function returns during its call:

```typescript
function add(left: number, right: number): number {
  return left + right;
}

const total = add(2, 3);
```

A delayed operation cannot return its final value immediately. It returns a Promise representing that future result:

```typescript
declare function loadTitle(): Promise<string>;
```

`Promise<string>` means the operation may later fulfill with a string. It may also reject with an error value.

## 2. Promise states

A Promise has one of three states:

- pending: not settled yet
- fulfilled: completed with a value
- rejected: failed with a reason

Fulfilled and rejected are both settled states. Once settled, a Promise does not switch to another state.

## 3. Handle fulfillment with `then`

```typescript
const titlePromise: Promise<string> = loadTitle();

titlePromise.then((title) => {
  console.log(title.toUpperCase());
});
```

The callback runs after fulfillment. TypeScript knows `title` is a string from `Promise<string>`.

The call to `then` itself returns another Promise. The callback result becomes the next fulfilled value:

```typescript
const lengthPromise = titlePromise.then((title) => title.length);
```

`lengthPromise` is `Promise<number>`.

## 4. Handle rejection with `catch`

```typescript
titlePromise
  .then((title) => {
    console.log(title);
  })
  .catch((error: unknown) => {
    if (error instanceof Error) {
      console.log(error.message);
    }
  });
```

A rejection earlier in the chain skips fulfillment handlers until a matching rejection handler is reached.

Promise catch callback parameters have historically been typed loosely by library declarations. Treat them as unknown in your code and narrow before use.

## 5. `finally` after settlement

```typescript
titlePromise
  .then((title) => console.log(title))
  .catch((error: unknown) => console.log("Failed", error))
  .finally(() => console.log("Request finished"));
```

Promise `finally` runs after fulfillment or rejection. It does not receive the result. Use it for completion indicators or cleanup attempts, not for transforming the value.

## 6. Wrap a timer

```typescript
function delay(milliseconds: number): Promise<void> {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, milliseconds);
  });
}

console.log("Before");

delay(100).then(() => {
  console.log("After delay");
});

console.log("Scheduled");
```

The output order is:

```text
Before
Scheduled
After delay
```

Creating the Promise starts the timer. The current synchronous code continues. The callback runs after the timer completes and the current work can yield to it.

## 7. Reject when the operation fails

```typescript
function requirePositiveLater(value: number): Promise<number> {
  return new Promise((resolve, reject) => {
    if (value <= 0) {
      reject(new Error("Expected a positive number"));
      return;
    }

    resolve(value);
  });
}
```

The Promise type parameter describes fulfillment. TypeScript does not currently encode one fixed rejection type in `Promise<T>`, so caught rejection values still need careful handling.

## 8. Promises are eager

The function passed to `new Promise` runs immediately during construction:

```typescript
const promise = new Promise<void>((resolve) => {
  console.log("Executor runs now");
  resolve();
});
```

Attaching `then` does not start this Promise. It attaches a reaction to work that has already started.

## 9. Asynchronous does not mean another CPU thread

Promises organize completion and continuation. They do not automatically move CPU-heavy loops to another thread. A long calculation can still block the JavaScript thread.

Separate worker APIs are used when work truly needs another thread or process.

## Common mistakes

### Treating a Promise as its fulfilled value

`Promise<string>` is not a string. Access the value through a handler or `await` in Module 27.

### Forgetting to return from a `then` callback

The next Promise then fulfills with undefined instead of the intended value.

### Leaving a rejection unhandled

Attach a purposeful handler or return the Promise to a caller that owns handling.

### Believing a Promise makes heavy computation nonblocking

It does not move the computation automatically.

## Check your understanding

1. What does `Promise<number>` describe?
2. What are the three Promise states?
3. What does `then` return?
4. When does a Promise executor run?
5. Does asynchronous code automatically use another CPU thread?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 27](../27-async-await-and-request-boundaries/README.md) uses `async` and `await` and validates data from network requests.
