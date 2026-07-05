# Question 04: Generic Inference & Type Parameters in Constraints (`keyof`)

Examine how TypeScript automatically infers generic type arguments, and how combining Generics with the `keyof` operator enforces 100% type-safe object property lookups.

## Code Scenario

Consider the following enterprise data-fetching helper designed to safely pluck a property value from a domain object:

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

interface Laptop {
  brand: string;
  ramGigabytes: number;
  isTouchscreen: boolean;
}

const workstation: Laptop = {
  brand: "ThinkPad",
  ramGigabytes: 32,
  isTouchscreen: false
};

const brandName = getProperty(workstation, "brand");
```

## Conceptual Questions

1. Notice that when calling `getProperty(workstation, "brand")`, we did not explicitly write angle brackets (`getProperty<Laptop, "brand">(...)`). Explain how **Generic Type Argument Inference** allows TypeScript to determine `T` and `K` automatically. What is the inferred type of `brandName`?
2. What exact structural rule does the constraint `K extends keyof T` enforce at compile time? What compile-time error occurs if a developer attempts to call `getProperty(workstation, "graphicsCard")`?
3. Why is the return type annotation written as indexed access `T[K]` rather than `any` or `unknown`? How does this protect enterprise state management engines from property lookup bugs?

## ANSWER HERE

> **1. Generic Type Argument Inference and inferred return type of `brandName`:**

> **2. Structural rule enforced by `K extends keyof T` and compile-time error analysis:**

> **3. Architectural meaning of indexed access return type `T[K]`:**
