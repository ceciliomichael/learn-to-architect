# Challenge 01: Solution

**Violations:**

1. Types, validation logic, data access logic, orchestration logic, and the entry point are all in a single file.
2. `orderDatabase` (data storage) lives in the same file as the business logic  -  this is a mixed data access layer.
3. `validateOrder` is domain/business logic that should be isolated from both data access and orchestration.
4. `createOrder` is an orchestrator  -  it coordinates validation and saving  -  but it mixes all concerns in one function.
5. The entry point `console.log(createOrder(...))` is mixed directly into the module body instead of an explicit `main` function.

**Refactored file structure:**
```
order-app/
├── types/index.ts           -  Shared interfaces (Order)
├── repositories/order.ts   -  Data access: in-memory storage and save function
├── services/order.ts       -  Business logic: validateOrder and createOrder
└── index.ts                -  Entry point
```

**File contents:**

```typescript
// types/index.ts

export interface Order {
  id: string;
  item: string;
  quantity: number;
  price: number;
}
```

---

```typescript
// repositories/order.ts

import { Order } from "../types";

const orderDatabase: Order[] = [];

export function saveOrder(order: Order): void {
  orderDatabase.push(order);
}

export function getAllOrders(): Order[] {
  return orderDatabase;
}
```

---

```typescript
// services/order.ts

import { Order } from "../types";
import { saveOrder } from "../repositories/order";

function validateOrder(order: Order): boolean {
  return order.quantity > 0 && order.price > 0 && order.item.length > 0;
}

export function createOrder(item: string, quantity: number, price: number): Order | null {
  const order: Order = { id: Date.now().toString(), item, quantity, price };
  if (!validateOrder(order)) {
    return null;
  }
  saveOrder(order);
  return order;
}
```

---

```typescript
// index.ts

import { createOrder } from "./services/order";

const result = createOrder("Book", 2, 15.99);
console.log(result);
```
