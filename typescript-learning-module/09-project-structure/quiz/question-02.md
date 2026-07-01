# Question 02: Circular Dependencies

What is a circular dependency? Why is it dangerous?

Imagine two files:

```typescript
// services/orderService.ts
import { logAction } from "./logService";
export function createOrder() { logAction("order created"); }

// services/logService.ts
import { getOrderCount } from "./orderService";
export function logAction(msg: string) { console.log(getOrderCount(), msg); }
```

1. Trace the circular dependency  -  why do these two files form a circle?
2. What might happen at runtime when Node.js tries to load these files?
3. How would you restructure this to break the cycle?

## ANSWER HERE

> **Why they form a circle:**

> **What might happen at runtime:**

> **How to break the cycle:**
