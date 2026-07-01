# Challenge 02: Fetch, Handle Errors, and Type the Response

Practice async error handling with typed interfaces.

## Starting Interface

```typescript
interface Product {
  id: number;
  name: string;
  price: number;
}
```

## Your Tasks

1. Write an async function `fetchProduct(id: number): Promise<Product>` that:
   - If `id < 1`, rejects with `new Error("Invalid product ID: " + id)`.
   - Otherwise, simulates a network delay (use `new Promise` with `setTimeout` of 300ms) and resolves with a mock `Product` object.

2. Write an async function `displayProduct(id: number): Promise<void>` that:
   - Calls `fetchProduct(id)` inside a `try` block.
   - On success: logs `"Product: " + product.name + " ($" + product.price + ")"`.
   - On error: checks `instanceof Error` and logs `"Error: " + error.message`.
   - Always logs `"Request finished."` in the `finally` block.

3. Call `displayProduct(1)` and `displayProduct(-1)` and observe the output.

## ANSWER HERE

```typescript
interface Product {
  id: number;
  name: string;
  price: number;
}

// Write fetchProduct and displayProduct here:


```
