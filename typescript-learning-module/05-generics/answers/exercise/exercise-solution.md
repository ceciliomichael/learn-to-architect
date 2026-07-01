# Module 05 Exercise Solutions

Reference implementations for Module 05 exercises.

---

### Solution 1: Generic Array First Element

```typescript
function getFirstElement<T>(arr: T[]): T | undefined {
  if (arr.length === 0) {
    return undefined;
  }
  return arr[0];
}

const firstStr = getFirstElement(["a", "b", "c"]); // inferred as string | undefined
const firstNum = getFirstElement([10, 20]); // inferred as number | undefined
```

---

### Solution 2: Generic Constraints

```typescript
function mergeNamedObjects<T extends { name: string }, U extends { name: string }>(
  obj1: T,
  obj2: U
): T & U {
  return { ...obj1, ...obj2 };
}

const userA = { name: "Alice", role: "Admin" };
const userB = { name: "Bob", department: "IT" };
const merged = mergeNamedObjects(userA, userB);

// Error: Property 'name' is missing in type '{ age: number }'
// mergeNamedObjects({ age: 25 }, userB);
```

---

### Solution 3: Generic Interfaces with Default Types

```typescript
interface PaginatedResponse<T = string> {
  data: T[];
  currentPage: number;
  totalPages: number;
}

// Uses default T = string
const stringResponse: PaginatedResponse = {
  data: ["Alpha", "Beta"],
  currentPage: 1,
  totalPages: 5
};

// Uses explicit T = { id: number; username: string }
const userResponse: PaginatedResponse<{ id: number; username: string }> = {
  data: [{ id: 1, username: "gamer99" }],
  currentPage: 2,
  totalPages: 10
};
```
