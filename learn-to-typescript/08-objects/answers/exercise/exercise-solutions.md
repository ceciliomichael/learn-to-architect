# Module 08 Exercise Solutions

## Warm-up solution

```typescript
const movie = {
  title: "Spirited Away",
  releaseYear: 2001,
  hasWatched: false,
};

console.log(`${movie.title} was released in ${movie.releaseYear}. Watched: ${movie.hasWatched}`);

movie.hasWatched = true;
console.log(movie.hasWatched);
```

The object remains assigned to the same `const` variable. Its writable boolean property changes.

## Guided exercise solution

```typescript
function printProduct(product: { name: string; price: number; inStock: boolean }) {
  console.log(`${product.name}: ${product.price} pesos`);

  if (product.inStock) {
    console.log("In stock");
  } else {
    console.log("Out of stock");
  }
}

printProduct({ name: "Pencil", price: 10, inStock: true });
printProduct({ name: "Eraser", price: 8, inStock: false });
```

The inline type states the minimum shape that this function needs.

## Independent exercise solution

```typescript
const inventory = [
  { name: "Pen", price: 12, quantity: 10 },
  { name: "Notebook", price: 45, quantity: 4 },
  { name: "Folder", price: 20, quantity: 6 },
];

let inventoryValue = 0;

for (const product of inventory) {
  const productValue = product.price * product.quantity;
  inventoryValue = inventoryValue + productValue;
}

console.log(inventoryValue);
```

The subtotal for each item is `120`, `180`, and `120`. Their sum is `420`.

## Reference exercise solution

Expected output:

```text
7
9
```

`sharedSettings` and `settings` refer to the same object, so changing through either name is visible through both. `copiedSettings` is a new outer object made with spread, so changing its `volume` does not change `settings.volume`.

## Debugging task solution

```typescript
const user = {
  name: "Rin",
  age: 23,
};

console.log(user.name);
user.age = 24;
console.log(user.age);
```

Object properties use colons in an object literal. Letter case matters in `user.name`. Starting `age` as a number lets it later receive another number.
