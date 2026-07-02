# Challenge 02: Discriminated Union State Machine & Exhaustiveness Guard

Senior interviewers often test if you can refactor error-prone boolean flags into compile-time guaranteed state machines.

## The Flawed Code (Boolean Flag Soup)

```typescript
interface AsyncData<T> {
  isLoading: boolean;
  isError: boolean;
  error?: string;
  data?: T;
}
```

## Your Tasks

1. In comments, list at least **4 impossible state combinations** allowed by the `AsyncData<T>` interface above (e.g., `isLoading: true, isError: true, data: [...]`). Explain why this is dangerous in UI or backend workflows.

2. Refactor `AsyncData<T>` into a strictly typed **Discriminated Union** called `RemoteData<T>` with 4 states: `"idle"`, `"loading"`, `"success"`, and `"failure"`. Ensure properties like `data` only exist on `"success"` and `error` only exists on `"failure"`.

3. Write a function `renderData<T>(state: RemoteData<T>, renderSuccess: (data: T) => string): string` using a `switch` statement on the discriminant.

4. Implement a `never` exhaustiveness check in the `default` case of the switch.

5. In comments, explain what happens during compilation if another developer adds `{ status: "refreshing"; previousData: T }` to `RemoteData<T>` two months later without updating `renderData`.

## ANSWER HERE

```typescript
// Write your explanation, RemoteData<T> union, renderData function, and exhaustiveness check here
```
