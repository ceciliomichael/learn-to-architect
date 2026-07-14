# Module 27: Async, Await, and Request Boundaries

## Before you start

Complete Modules 01 to 26. You should understand Promises and runtime validation.

## What you will learn

- write and type an `async` function
- pause an async function with `await`
- handle rejected Promises
- check HTTP responses and validate response data
- compare sequential and parallel work
- use `Promise.all` and `Promise.allSettled`

## Why this matters

`async` and `await` make Promise workflows read in execution order. They do not remove the need for error handling, response checks, or runtime validation.

## 1. An async function always returns a Promise

```typescript
async function getCount(): Promise<number> {
  return 5;
}
```

Returning `5` fulfills the returned Promise with `5`. Returning a Promise causes the async function to adopt its final state.

This is a type error:

```typescript
// Intentional error: async functions do not return plain number.
async function getCount(): number {
  return 5;
}
```

## 2. Await a Promise

```typescript
async function printDelayedTitle(): Promise<void> {
  const title = await Promise.resolve("TypeScript");
  console.log(title.toUpperCase());
}
```

`await` pauses this async function until the Promise settles. It does not block the entire JavaScript process while the external operation is pending.

If the Promise rejects, `await` throws inside the async function.

## 3. Handle async failure

```typescript
async function run(): Promise<void> {
  try {
    const value = await riskyAsyncOperation();
    console.log(value);
  } catch (error: unknown) {
    if (error instanceof Error) {
      console.log(error.message);
    }
  }
}
```

Callers must still handle the Promise returned by `run` when a failure can escape it.

Do not start an async operation and silently discard its Promise. Await it, return it, or deliberately attach a handler.

## 4. Fetch checks transport success separately

```typescript
async function fetchValue(url: string): Promise<unknown> {
  const response = await fetch(url);

  if (!response.ok) {
    throw new Error(`Request failed with status ${response.status}`);
  }

  const data: unknown = await response.json();
  return data;
}
```

`fetch` normally rejects for network-level failure. An HTTP status such as 404 still produces a Response, so check `response.ok` or the status explicitly.

Parsed response data is unknown until validated.

## 5. Validate the response shape

```typescript
interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

function isTodo(value: unknown): value is Todo {
  if (typeof value !== "object" || value === null || Array.isArray(value)) {
    return false;
  }

  const record = value as { [key: string]: unknown };
  return (
    typeof record["id"] === "number" &&
    typeof record["title"] === "string" &&
    typeof record["completed"] === "boolean"
  );
}

async function fetchTodo(url: string): Promise<Todo> {
  const value = await fetchValue(url);

  if (!isTodo(value)) {
    throw new Error("Response does not match Todo");
  }

  return value;
}
```

The localized assertion creates an indexable view only after the runtime object checks. The property checks provide the evidence for the returned type predicate.

## 6. Sequential work

```typescript
const first = await loadOne();
const second = await loadTwo(first.id);
```

This must be sequential because the second operation needs the first result.

Do not run dependent work in parallel.

## 7. Parallel independent work

```typescript
const firstPromise = loadFirst();
const secondPromise = loadSecond();

const [first, second] = await Promise.all([firstPromise, secondPromise]);
```

Both operations start before either is awaited. `Promise.all` preserves result order, not completion order.

If any input rejects, the returned Promise rejects. Other underlying operations are not automatically cancelled.

## 8. Collect every settlement

```typescript
const results = await Promise.allSettled([
  loadFirst(),
  loadSecond(),
]);

for (const result of results) {
  if (result.status === "fulfilled") {
    console.log(result.value);
  } else {
    console.log(result.reason);
  }
}
```

Use `allSettled` when every outcome matters even if some operations fail. Its result is a discriminated union narrowed by `status`.

## 9. Cancellation is separate

Promises do not have built-in universal cancellation. APIs such as `fetch` accept an `AbortSignal`:

```typescript
const controller = new AbortController();
const request = fetch(url, { signal: controller.signal });
controller.abort();
```

Aborting is API behavior, not a feature every Promise automatically supports.

## Common mistakes

### Returning a plain type annotation from an async function

Use `Promise<T>`.

### Assuming `fetch` rejects for every HTTP error status

Check the Response status.

### Trusting `response.json()` as a typed domain object

Store it as unknown and validate.

### Awaiting independent tasks one at a time

Start them together when they are truly independent and parallelism is desired.

## Check your understanding

1. What does an async function return?
2. What happens when an awaited Promise rejects?
3. Why check `response.ok`?
4. Does parsing JSON validate a Todo shape?
5. How do `Promise.all` and `Promise.allSettled` differ?

## Practice

Complete the [module exercises](./exercise/exercise.md), then take the [module quiz](./quiz/quiz.md).

## Next step

[Module 28](../28-discriminated-unions-and-state/README.md) models asynchronous and application states without impossible property combinations.
