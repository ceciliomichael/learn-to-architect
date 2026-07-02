# Challenge 03: Solution

```typescript
const products = [
  { name: "Sword",  price: 150, inStock: true  },
  { name: "Potion", price: 25,  inStock: false },
  { name: "Shield", price: 200, inStock: true  },
  { name: "Arrow",  price: 5,   inStock: true  },
  { name: "Helmet", price: 175, inStock: false }
];

// Step 1: Filter to only in-stock products
const availableProducts = products.filter((product) => product.inStock === true);

// Step 2: Map each product to a formatted label string
const productLabels = availableProducts.map(
  (product) => `${product.name} - $${product.price}`
);

// Step 3: Log each label
productLabels.forEach((label) => {
  console.log(label);
});
// Outputs
// Sword - $150
// Shield - $200
// Arrow - $5

// Step 4: Log the total count of available products
console.log("Available:", availableProducts.length); // 3
```
