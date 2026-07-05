# Question 01: keyof

What does `keyof` do?

```typescript
interface Product {
  id: number;
  name: string;
  price: number;
  inStock: boolean;
}

type ProductKey = keyof Product;
```

1. What is the exact resolved type of `ProductKey`?
2. If you declare `let key: ProductKey`, what values can you assign to it?
3. What TypeScript error do you get if you write `let badKey: ProductKey = "discount"`?

## ANSWER HERE

> **Exact type of `ProductKey`:**

> **Valid values for `let key: ProductKey`:**

> **Error for `"discount"`:**
