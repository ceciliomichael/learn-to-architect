# Question 01 Answer

**Correct answer: C**  -  TypeScript automatically merges them into one combined interface.

This is called **declaration merging**. When two `interface` declarations share the same name in the same scope, TypeScript silently combines all their properties into a single unified contract
```typescript
interface UserSettings { theme: string; }
interface UserSettings { fontSize: number; }

// TypeScript sees this as: { theme: string; fontSize: number; }
const settings: UserSettings = { theme: "dark", fontSize: 16 };
```

With `type` aliases, this is impossible. Declaring the same `type` name twice is a hard compiler error
```
Duplicate identifier 'UserSettings'.
```

Declaration merging is useful when augmenting types from external libraries, but in your own code it can be surprising if done accidentally.
