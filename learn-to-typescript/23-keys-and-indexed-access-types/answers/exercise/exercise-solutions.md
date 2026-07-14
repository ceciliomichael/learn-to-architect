# Module 23 Exercise Solutions

## Exercises 1 and 2

```typescript
interface Product {
  id: string;
  name: string;
  price: number;
  inStock: boolean;
}

type ProductKey = keyof Product;
type ProductName = Product["name"];
type ProductPrice = Product["price"];
type ProductValue = Product[keyof Product];
```

`ProductValue` is `string | number | boolean`.

## Exercise 3

```typescript
function getProperty<T, K extends keyof T>(object: T, key: K): T[K] {
  return object[key];
}

const product: Product = {
  id: "p1",
  name: "Pen",
  price: 12,
  inStock: true,
};

const name = getProperty(product, "name");
const price = getProperty(product, "price");
```

An invalid key is rejected because it does not satisfy `keyof Product`.

## Exercises 4 and 5

```typescript
const defaultPreferences = {
  theme: "light",
  fontSize: 16,
  reducedMotion: false,
};

type Preferences = typeof defaultPreferences;

const preferences: Preferences = {
  theme: "dark",
  fontSize: 18,
  reducedMotion: true,
};
```

Runtime `typeof defaultPreferences` returns the string `"object"`. Type-position `typeof defaultPreferences` creates the static object type used by `Preferences`.
