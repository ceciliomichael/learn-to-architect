# Question 01 Answer

**Exact type of `ProductKey`:**
```typescript
"id" | "name" | "price" | "inStock"
```
`keyof Product` extracts all property names of `Product` as a literal string union.

**Valid values for `let key: ProductKey`:**
`"id"`, `"name"`, `"price"`, or `"inStock"`. Nothing else.

**Error for `"discount"`:**
```
Type '"discount"' is not assignable to type 'keyof Product'.
```
Because `"discount"` is not one of the actual property names of `Product`, TypeScript rejects it.
