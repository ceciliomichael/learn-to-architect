# Question 05 Answer: Union vs. Intersection  -  Real-World Analogy

## Answer

### Part 1  -  Union type (`|`)

**What it guarantees:** A union type means a value is exactly one of the listed types  -  TypeScript cannot know which one without a narrowing check, so it only lets you use features guaranteed to exist on *every* member.

**Real-world analogy:** A union type is like a parcel that might contain either a book or a DVD  -  you have to open the box and look inside before you know which one it is or can interact with it specifically.

---

### Part 2  -  Intersection type (`&`)

**What it guarantees:** An intersection type means a value simultaneously satisfies *all* listed types  -  every property and method from every member is guaranteed to be present.

**Real-world analogy:** An intersection type is like a person who is *both* a licensed doctor *and* a licensed lawyer  -  they carry the full qualifications and responsibilities of both roles at the same time, with no need to check which one they are.

---

### Part 3  -  Property access analysis

```typescript
type WithEngine = { horsepower: number; startEngine(): void };
type WithSails  = { sailArea: number;   hoist(): void };

declare const u: WithEngine | WithSails;
declare const i: WithEngine & WithSails;
```

#### `u: WithEngine | WithSails` (union)

TypeScript can only guarantee properties that are present on **every member** of the union. Looking at the two types:

| Property / Method | `WithEngine` | `WithSails` | On all members? |
|---|---|---|---|
| `horsepower` | ✅ | ❌ | ❌  -  unsafe |
| `startEngine()` | ✅ | ❌ | ❌  -  unsafe |
| `sailArea` | ❌ | ✅ | ❌  -  unsafe |
| `hoist()` | ❌ | ✅ | ❌  -  unsafe |

**None** of the four properties are common to both types, so accessing any of them on `u` without narrowing is a compile-time error. You must use `in` or another narrowing technique first:

```typescript
// ERROR on every line below without narrowing:
u.horsepower;    // ❌
u.startEngine(); // ❌
u.sailArea;      // ❌
u.hoist();       // ❌

// Safe after narrowing:
if ('horsepower' in u) {
  u.startEngine(); // ✅ TypeScript narrows u to WithEngine
}
```

#### `i: WithEngine & WithSails` (intersection)

The intersection *requires* the value to have **all** properties from **both** types simultaneously. Every property is guaranteed:

```typescript
i.horsepower;    // ✅ Safe  -  from WithEngine
i.startEngine(); // ✅ Safe  -  from WithEngine
i.sailArea;      // ✅ Safe  -  from WithSails
i.hoist();       // ✅ Safe  -  from WithSails
```

No narrowing is needed at all. Think of `i` as a hybrid vessel that has both an engine and sails.
