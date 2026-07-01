# Challenge 02: Solution

```typescript
function printName<T extends { name: string }>(item: T): void {
  console.log(item.name);
}

function mergeObjects<T extends object, U extends object>(a: T, b: U): T & U {
  return { ...a, ...b };
}

// Test printName:
printName({ name: "Alice", age: 30 }); // "Alice"  -  works, object has 'name'

// printName({ age: 30 });
// ERROR: Argument of type '{ age: number }' is not assignable to parameter of type '{ name: string }'.
// Property 'name' is missing.

// Test mergeObjects:
const merged = mergeObjects({ id: 1, role: "admin" }, { name: "Alice", active: true });
// TypeScript infers return type as: { id: number; role: string; } & { name: string; active: boolean; }
console.log(merged);
// { id: 1, role: "admin", name: "Alice", active: true }
```
