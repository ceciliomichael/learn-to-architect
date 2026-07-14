# Module 33 Exercise Solutions

## Exercises 1 and 2

```typescript
const permissions = ["read", "write", "delete"] as const;
type Permission = (typeof permissions)[number];

const labels = {
  read: "Read items",
  write: "Change items",
  delete: "Delete items",
} satisfies Record<Permission, string>;
```

## Exercise 3

The broad `Record<string, string>` annotation describes any string key, so it can lose the expression's exact key union in the variable type. `satisfies` checks the record constraint while retaining the known keys from the object expression.

## Exercise 4

```typescript
declare const productIdBrand: unique symbol;
type ProductId = string & { readonly [productIdBrand]: true };

function parseProductId(value: string): ProductId | undefined {
  return value.startsWith("product_") ? value as ProductId : undefined;
}

function loadProduct(id: ProductId): void {
  console.log(id);
}
```

The assertion is kept inside the validating constructor.

## Exercise 5

```typescript
const handleAnimal: (animal: Animal) => void = (animal) => {
  console.log(animal.name);
};
```

A general caller may send a non-Dog Animal, so a Dog-only function would not be safe.
