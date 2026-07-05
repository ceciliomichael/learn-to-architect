# Challenge 03: Array Transformation Pipeline

Chain `.filter()`, `.map()`, and `.forEach()` together on a product list.

## Starting Data

```typescript
const products = [
  { name: "Sword",   price: 150, inStock: true  },
  { name: "Potion",  price: 25,  inStock: false },
  { name: "Shield",  price: 200, inStock: true  },
  { name: "Arrow",   price: 5,   inStock: true  },
  { name: "Helmet",  price: 175, inStock: false }
];
```

## Your Tasks

1. Use `.filter()` to get only the products where `inStock` is `true`. Store the result in `availableProducts`.
2. Use `.map()` on `availableProducts` to create a new array of strings. Each string should be formatted as `"NAME: $PRICE"` (e.g. `"Sword: $150"`). Store in `productLabels`.
3. Use `.forEach()` on `productLabels` to log each label.
4. Log the total count of available products using `.length`.

## ANSWER HERE

```typescript
const products = [
  { name: "Sword",   price: 150, inStock: true  },
  { name: "Potion",  price: 25,  inStock: false },
  { name: "Shield",  price: 200, inStock: true  },
  { name: "Arrow",   price: 5,   inStock: true  },
  { name: "Helmet",  price: 175, inStock: false }
];

// Write your filter, map, and forEach chains here
```
