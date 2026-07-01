# Challenge 01: Solution

```typescript
function describeInput(value: string | number | boolean): string {
  if (typeof value === "string") {
    return `Text with ${value.length} characters: ${value}`;
  } else if (typeof value === "number") {
    return value.toFixed(2);
  } else {
    return value === true ? "Enabled" : "Disabled";
  }
}

console.log(describeInput("TypeScript")); // "Text with 10 characters: TypeScript"
console.log(describeInput(9.9));          // "9.90"
console.log(describeInput(true));         // "Enabled"
console.log(describeInput(false));        // "Disabled"
```
