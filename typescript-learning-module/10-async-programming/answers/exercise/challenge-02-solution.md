# Challenge 02: Solution

```typescript
interface Product {
  id: number;
  name: string;
  price: number;
}

async function fetchProduct(id: number): Promise<Product> {
  if (id < 1) {
    throw new Error("Invalid product ID: " + id);
  }
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve({ id, name: "TypeScript Handbook", price: 29.99 });
    }, 300);
  });
}

async function displayProduct(id: number): Promise<void> {
  try {
    const product = await fetchProduct(id);
    console.log("Product: " + product.name + " ($" + product.price + ")");
  } catch (error) {
    if (error instanceof Error) {
      console.log("Error: " + error.message);
    }
  } finally {
    console.log("Request finished.");
  }
}

displayProduct(1);  // "Product: TypeScript Handbook ($29.99)"  then "Request finished."
displayProduct(-1); // "Error: Invalid product ID: -1"          then "Request finished."
```
