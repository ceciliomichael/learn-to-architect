# Challenge 01: The tsconfig.json Cockpit Audit and Fix

In this challenge, you will step into the role of a Principal TypeScript Architect. You have just been hired to audit an enterprise e-commerce backend service that has been experiencing unexplained runtime crashes in production (`TypeError: Cannot read properties of null` and `undefined is not a function`), slow build times, and disorganized deployment artifacts.

After investigating the codebase, you discover that the root cause of these issues lies in a deeply flawed `tsconfig.json` file and loosely typed TypeScript source code.

## The Flawed Configuration and Code

### 1. Legacy `tsconfig.json`
```json
{
  "compilerOptions": {
    "target": "ES5",
    "module": "CommonJS",
    "sourceMap": false,
    "strict": false,
    "noImplicitAny": false,
    "strictNullChecks": false,
    "noUncheckedIndexedAccess": false
  }
}
```

### 2. Flawed Source Code (`src/orderProcessor.ts`)
```typescript
interface OrderItem {
  sku: string;
  price: number;
  discountCode?: string;
}

interface Order {
  orderId: string;
  customerEmail: string | null;
  items: OrderItem[];
}

// Flaw 1: Parameter has no type annotation
function calculateTotal(items) {
  let total = 0;
  for (let i = 0; i < items.length; i++) {
    total += items[i].price;
  }
  return total;
}

// Flaw 2: Unsafe null access and out-of-bounds array access
function getFirstItemSku(order: Order): string {
  // Accessing email without checking if it is null
  console.log("Processing order for: " + order.customerEmail.toLowerCase());
  
  // Accessing index 0 without checking if the array is empty
  const firstItem = order.items[0];
  
  // Accessing property on potentially undefined array element
  return firstItem.sku;
}
```

## Your Tasks

1. **Audit Report**: Identify and explain at least 5 critical configuration and architectural flaws in the legacy `tsconfig.json` and source code. For each flaw, explain what runtime risk or development bottleneck it creates.
2. **Production `tsconfig.json`**: Write a complete, enterprise-ready `tsconfig.json` file that activates all autopilot safety shields (`strict`, `noImplicitAny`, `strictNullChecks`, `noUncheckedIndexedAccess`), configures proper file routing (`rootDir: "./src"`, `outDir: "./dist"`), enables debugging (`sourceMap: true`), and sets modern language targets (`ES2022` or `ESNext`).
3. **Refactored Source Code**: Rewrite `src/orderProcessor.ts` so that it compiles with zero errors under your strict configuration. You must add explicit type annotations, handle potential `null` values safely, and guard against potential `undefined` results from array indexing.

---

## ANSWER HERE

### 1. Audit Report (5 Critical Flaws)

1. **Flaw 1**: 
   * **Risk/Impact**: 

2. **Flaw 2**: 
   * **Risk/Impact**: 

3. **Flaw 3**: 
   * **Risk/Impact**: 

4. **Flaw 4**: 
   * **Risk/Impact**: 

5. **Flaw 5**: 
   * **Risk/Impact**: 

### 2. Production `tsconfig.json`

```json
{
  "compilerOptions": {
    // Write your production configuration here
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

### 3. Refactored Source Code (`src/orderProcessor.ts`)

```typescript
// Write your fully type-safe, strict-compliant TypeScript implementation here
```
