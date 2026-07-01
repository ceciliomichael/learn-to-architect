# Challenge 01: Solution

```typescript
function parseJSON(input: string): object {
  try {
    return JSON.parse(input) as object;
  } catch (error) {
    if (error instanceof Error) {
      throw new Error("Invalid JSON: " + error.message);
    }
    throw new Error("Invalid JSON: Unknown error.");
  } finally {
    console.log("Parse attempt finished.");
  }
}

async function safeParseJSON(input: string): Promise<object | null> {
  try {
    const result = parseJSON(input);
    return result;
  } catch (error) {
    if (error instanceof Error) {
      console.log("Caught: " + error.message);
    }
    return null;
  }
}

// Test with valid JSON:
safeParseJSON('{"name": "Alice", "age": 30}').then((result) => {
  console.log("Valid result:", result);
});

// Test with invalid JSON:
safeParseJSON("this is not json").then((result) => {
  console.log("Invalid result:", result); // null
});
```
