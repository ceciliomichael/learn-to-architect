# Question 05 Answer

```typescript
// 1. Split the string into an array of three strings
const parts = "10,20,30".split(",");
// Result: ["10", "20", "30"]

// 2. Access the second item (index 1)
const secondItem = parts[1]; // "20"

// 3. Log it in uppercase (same concept even though numbers have no lowercase)
console.log(secondItem.toUpperCase()); // "20"

// 4. Bonus: Convert to an actual number using parseInt
const asNumber = parseInt(secondItem);
console.log(asNumber);        // 20 (a number, not a string)
console.log(typeof asNumber); // "number"
```

Key point: Array indexes start at `0`. So the first item is `parts[0]`, the second item is `parts[1]`, and the third item is `parts[2]`.
