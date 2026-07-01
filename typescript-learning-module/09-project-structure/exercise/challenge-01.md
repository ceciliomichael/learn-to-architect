# Challenge 01: Identify the Architecture Violations

Read the code below and identify every architectural problem, then refactor it into properly separated files.

## The Bad Code

```typescript
// app.ts  -  everything in one file

interface Order {
  id: string;
  item: string;
  quantity: number;
  price: number;
}

const orderDatabase: Order[] = [];

function validateOrder(order: Order): boolean {
  return order.quantity > 0 && order.price > 0 && order.item.length > 0;
}

function saveOrder(order: Order): void {
  orderDatabase.push(order);
}

function createOrder(item: string, quantity: number, price: number): Order | null {
  const order: Order = { id: Date.now().toString(), item, quantity, price };
  if (!validateOrder(order)) {
    console.log("Invalid order");
    return null;
  }
  saveOrder(order);
  return order;
}

console.log(createOrder("Book", 2, 15.99));
```

## Your Tasks

1. List every architectural violation as numbered bullet points (at least 4 violations).
2. Propose the refactored file structure. Write each file path and a one-sentence responsibility comment.
3. Write the full content of each file in your answer.

## ANSWER HERE

**Violations:**

1.

**Refactored file structure:**

**File contents:**

```typescript
// Write each file separated by --- and a filename comment

```
