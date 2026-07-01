# Challenge 01: Solution

```typescript
function getFirstElement<T>(arr: T[]): T | undefined {
  if (arr.length === 0) return undefined;
  return arr[0];
}

// Test 1: string array  -  TypeScript infers return type as string | undefined
const firstFruit = getFirstElement(["apple", "banana", "cherry"]);
console.log(firstFruit); // "apple"

// Test 2: number array  -  TypeScript infers return type as number | undefined
const firstScore = getFirstElement([95, 82, 100]);
console.log(firstScore); // 95

// Test 3: empty array  -  must specify T explicitly
const fromEmpty = getFirstElement<string>([]);
console.log(fromEmpty); // undefined
```
