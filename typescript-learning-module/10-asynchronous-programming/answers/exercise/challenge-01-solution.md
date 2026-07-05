# Challenge 01: Solution

```typescript
function simulateDelay(ms: number): Promise<string> {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Done after " + ms + "ms");
    }, ms);
  });
}

async function main(): Promise<void> {
  const result1 = await simulateDelay(500);
  console.log(result1); // "Done after 500ms"

  const result2 = await simulateDelay(200);
  console.log(result2); // "Done after 200ms"
}

// Calling main() starts the async function and returns a Promise.
// We do not need to await it at the top level in a script file.
main();

// Note: 'await main()' would only be valid inside another async function,
// or at the top level of a file with "type": "module" in package.json.
```
