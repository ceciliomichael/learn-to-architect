# Solution  -  Challenge 02: Discriminated Union State Machine

## 1. Impossible State Combinations in Boolean Flag Soup

With `isLoading: boolean, isError: boolean, error?: string, data?: T`, the following illegal states can exist
1. `{ isLoading: true, isError: true }`  -  Can an app be actively loading while simultaneously showing a terminal error screen?
2. `{ isLoading: true, data: [...] }`  -  Is this initial loading or background refreshing? Should the UI show a spinner or a table?
3. `{ isError: true, error: undefined }`  -  Flag says error, but there is no message to render.
4. `{ isLoading: false, isError: false, data: undefined }`  -  App is neither loading, errored, nor successful. What is rendered?

In UI workflows, these impossible states lead to flicker, race conditions, and unhandled `undefined` crashes.

---

## 2. Refactored Discriminated Union & Exhaustiveness Guard

```typescript
export type RemoteData<T> =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: T }
  | { status: "failure"; error: string };

export function renderData<T>(
  state: RemoteData<T>,
  renderSuccess: (data: T) => string
): string {
  switch (state.status) {
    case "idle"
      return "Ready to load data.";
    case "loading"
      return "Loading spinner...";
    case "success"
      // TypeScript automatically narrows state to have .data here
      return renderSuccess(state.data);
    case "failure"
      // TypeScript narrows state to have .error here
      return `Error: ${state.error}`;
    default
      // If someone adds { status: "refreshing" } to RemoteData<T> later,
      // TypeScript raises a compile error right here because "refreshing" is not assignable to 'never'.
      const _exhaustiveCheck: never = state;
      return _exhaustiveCheck;
  }
}
```
