# Module 05 Exercise Solutions Master Reference

This master reference document provides exhaustive, production-grade solutions for all Module 05 lab exercises. Each implementation demonstrates enterprise TypeScript standards, zero reliance on `any`, complete structural type safety, and symbol-by-symbol clarity.

---

## Challenge 01 Solution: Generic Safe Getter

### Problem Statement
Create a universal function `getFirstElement<T>(arr: T[]): T | undefined` that safely retrieves the first item of an array without throwing runtime exceptions on empty arrays.

### Production Implementation
```typescript
function getFirstElement<T>(arr: T[]): T | undefined {
  if (arr.length === 0) {
    return undefined;
  }
  return arr[0];
}

// Verification Tests:
const firstStr: string | undefined = getFirstElement(["alpha", "beta", "gamma"]);
const firstNum: number | undefined = getFirstElement([100, 200, 300]);
const firstEmpty: string | undefined = getFirstElement<string>([]);

console.log("String result:", firstStr);   // Output: "alpha"
console.log("Number result:", firstNum);   // Output: 100
console.log("Empty result:", firstEmpty);  // Output: undefined
```

### Architectural Takeaways
* **Generic Inference**: TypeScript automatically infers `T` from the argument array elements. For `["alpha", "beta"]`, `T` is inferred as `string`.
* **Explicit Parameterization**: For empty array literals `[]`, passing `<string>` explicitly prevents TypeScript from falling back to `never[]` or `any[]`.

---

## Challenge 02 Solution: Generic Constraints with extends

### Problem Statement
Implement a constrained function `printName<T extends { name: string }>(item: T): void` and an intersection merging utility `mergeObjects<T extends object, U extends object>(a: T, b: U): T & U`.

### Production Implementation
```typescript
function printName<T extends { name: string }>(item: T): void {
  console.log("Entity Name:", item.name);
}

function mergeObjects<T extends object, U extends object>(a: T, b: U): T & U {
  return { ...a, ...b };
}

// Verification Tests:
printName({ name: "Alice", role: "Admin", active: true }); // Valid structural match!

interface Account {
  accountId: string;
}
interface Balance {
  amountCurrency: number;
}

const account: Account = { accountId: "ACC-9901" };
const balance: Balance = { amountCurrency: 5000 };

const accountBalance: Account & Balance = mergeObjects(account, balance);
console.log("Merged Account Balance:", accountBalance);
// Output: { accountId: 'ACC-9901', amountCurrency: 5000 }
```

### Architectural Takeaways
* **Structural Duck Typing**: The constraint `T extends { name: string }` accepts any object shape as long as it possesses at least a `name` string property.
* **Primitive Protection**: Constraining `<T extends object, U extends object>` prevents accidental primitive spreading (such as passing numbers or booleans into object spread engines).

---

## Challenge 03 Solution: Generic Interface with Default Type

### Problem Statement
Design an API wrapper blueprint `ApiResponse<T = string>` that defaults simple responses to strings while allowing domain models to override the payload slot.

### Production Implementation
```typescript
interface ApiResponse<T = string> {
  success: boolean;
  data: T;
  errorMessage: string | null;
}

// Verification Tests:
const statusLog: ApiResponse = {
  success: true,
  data: "Server connection established successfully.",
  errorMessage: null
};

const errorCode: ApiResponse<number> = {
  success: false,
  data: 503,
  errorMessage: "Service Unavailable"
};

interface UserPayload {
  userId: number;
  emailAddress: string;
}

const userFetch: ApiResponse<UserPayload> = {
  success: true,
  data: {
    userId: 8821,
    emailAddress: "architect@enterprise.org"
  },
  errorMessage: null
};

console.log("Status Data:", statusLog.data);
console.log("User Email:", userFetch.data.emailAddress);
```

### Architectural Takeaways
* **Ergonomic Defaulting**: The syntax `= string` acts as a fallback type, allowing developers to omit angle brackets for standard text endpoints while retaining polymorphism for complex domain models.
* **Zero Boilerplate**: This design pattern prevents "Generic Fatigue" across large frontend and backend codebases.

---

## Summary of Best Practices for Module 05 Exercises

| Principle | Anti-Pattern | Senior Engineering Standard |
| :--- | :--- | :--- |
| **Type Safety** | Using `any` to bypass compiler checks. | Capturing exact input types with generic variables `<T>`. |
| **Property Access** | Accessing `.length` or `.name` on raw unconstrained `<T>`. | Applying structural constraints via `<T extends Blueprint>`. |
| **Object Merging** | Allowing primitive values into object merging tools. | Constraining type variables with `<T extends object>`. |
| **Library Ergonomics** | Forcing explicit `<string>` parameterization on trivial endpoints. | Providing intelligent fallback defaults with `<T = string>`. |
