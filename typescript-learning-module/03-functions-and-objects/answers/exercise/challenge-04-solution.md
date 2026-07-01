# Challenge 04: Solution

```typescript
function calculateTotal(...numbers: number[]): number {
  let total = 0;
  for (let num of numbers) {
    total = total + num;
  }
  return total;
}

function joinWords(...words: string[]): string {
  let result = "";
  for (let i = 0; i < words.length; i++) {
    if (i === 0) {
      result = words[i];
    } else {
      result = result + " " + words[i];
    }
  }
  return result;
}

console.log(calculateTotal(10, 20, 30, 40, 50)); // 150
console.log(joinWords("TypeScript", "is", "really", "great")); // "TypeScript is really great"
```
