# Module 24 Exercise Solutions

## Exercise 1

```typescript
type NewProduct = Omit<Product, "id">;
type ProductSummary = Pick<Product, "id" | "name" | "price">;
type ProductUpdate = Partial<Pick<Product, "name" | "price" | "description" | "inStock">>;
type ReadonlyProduct = Readonly<Product>;
```

The update type lists only fields the operation permits changing.

## Exercise 2

```typescript
type StockState = "available" | "low" | "empty";

const stockLabels: Record<StockState, string> = {
  available: "Available",
  low: "Low stock",
  empty: "Out of stock",
};
```

## Exercise 3

```typescript
type Nullable<T> = {
  [Key in keyof T]: T[Key] | null;
};
```

## Exercise 4

```typescript
function toProductSummary(product: Product): ProductSummary {
  return {
    id: product.id,
    name: product.name,
    price: product.price,
  };
}
```

The function performs the runtime transformation. The utility only described its result.

## Exercise 5

An explicit interface is often clearer when it is short, public, and carries domain meaning. Utility composition is strongest when the relationship to a source model is important and remains readable.
