# Exercise Solution: Async Ownership, Abort Signals, Timeouts, and Stale Results

```ts
let current: AbortController | null = null;

async function search(query: string): Promise<void> {
  current?.abort();
  const controller = new AbortController();
  current = controller;

  try {
    const url = new URL("/api/search", location.origin);
    url.searchParams.set("q", query);
    const response = await fetch(url, { signal: controller.signal });
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const data: unknown = await response.json();

    if (current === controller) console.log(data);
  } catch (error) {
    if (!(error instanceof DOMException && error.name === "AbortError")) {
      throw error;
    }
  }
}
```

## Why this works

The example implements the module's smallest complete boundary. Adapted values are valid when they preserve null checks, runtime validation, lifecycle ownership, accessible HTML, and explicit failure behavior.

