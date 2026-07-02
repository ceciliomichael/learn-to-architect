# Module 02 Exercise Solutions

Check your solutions against these reference implementations.

---

### Solution 1: E-Commerce Cart Blueprint

```typescript
interface CartItem {
  readonly id: string;
  title: string;
  price: number;
  discountCode?: string;
  tags: string[];
}

const myCartItem: CartItem = {
  id: "item-101",
  title: "Mechanical Keyboard",
  price: 89.99,
  tags: ["peripherals", "sale"]
};

// Cannot assign to 'id' because it is a read-only property.
// myCartItem.id = "item-102";
```

---

### Solution 2: Index Signatures

```typescript
interface Dictionary {
  [key: string]: string;
}

const frenchDict: Dictionary = {
  hello: "bonjour",
  goodbye: "au revoir",
  cat: "chat"
};

// Error: Type 'number' is not assignable to type 'string'.
// Because our index signature requires all values to be strings
// frenchDict.wordCount = 100;
```

---

### Solution 3: Type vs. Interface Extension

```typescript
// Using interface (extends)
interface Animal {
  name: string;
  age: number;
}

interface Bird extends Animal {
  canFly: boolean;
}

// Using type (intersection &)
type TypeAnimal = {
  name: string;
  age: number;
};

type TypeBird = TypeAnimal & {
  canFly: boolean;
};
```
