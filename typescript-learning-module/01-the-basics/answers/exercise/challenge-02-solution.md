# Challenge 02: Solution - Build a Typed Inventory

```typescript
let itemNames: string[]  = ["Sword", "Shield", "Potion"];
let itemDamage: number[] = [120, 0, 0];
let isEquipped: boolean[] = [true, true, false];

// First item name (index 0)
console.log(itemNames[0]); // "Sword"

// Total count using .length
console.log(itemNames.length); // 3

// Second item name in uppercase (index 1)
console.log(itemNames[1].toUpperCase()); // "SHIELD"

// Push a fourth item and log the updated length
itemNames.push("Arrow");
console.log(itemNames.length); // 4
```
