# Challenge 03: Type-Only Imports (`import type`) and Clean Barrel Files (`index.ts`)

In large TypeScript codebases and monorepos, improper import practices can lead to severe build bloat and runtime performance degradation. When frontend components import runtime classes or backend database services merely to reference their TypeScript interface shapes, standard imports can trick JavaScript build bundlers into bundling heavy server-side code into the client browser bundle!

Furthermore, messy multi-line imports across deeply nested folders create friction. The solution is combining **Type-Only Imports (`import type`)** with clean **Barrel Files (`index.ts`)**.

## The Scenario

You are optimizing the build pipeline for an enterprise cloud management dashboard. Your domain models are currently scattered across multiple files. Frontend dashboard views need to import TypeScript interfaces (`UserProfile`, `OrderRecord`) without importing heavy runtime validation engines (`UserValidatorClass`, `OrderProcessingEngine`) that depend on Node.js filesystem modules.

You need to architect a clean folder structure with a centralized **Barrel File (`index.ts`)** and enforce strict **Type-Only Imports** in consuming client services.

## Your Task

Write your complete solution directly inside the **ANSWER HERE** block below. Your solution must include four distinct sections:

1. **Section 1: Domain Model File 1 (`src/models/userProfile.ts`)**
   - Export an interface `UserProfile` with properties `userId: string`, `email: string`, and `role: "ADMIN" | "USER"`.
   - Export a type alias `UserPermissions` representing an array of permission strings.
   - Export a runtime class `UserValidatorClass` with a static method `validateEmail(email: string): boolean`.

2. **Section 2: Domain Model File 2 (`src/models/orderHistory.ts`)**
   - Export an interface `OrderRecord` with properties `orderId: string`, `totalAmount: number`, and `timestamp: Date`.
   - Export a type alias `OrderStatus` with union values `"PENDING" | "COMPLETED" | "CANCELLED"`.
   - Export a runtime class `OrderProcessingEngine` with a method `processOrder(order: OrderRecord): boolean`.

3. **Section 3: The Central Barrel File (`src/models/index.ts`)**
   - Write a clean barrel file that acts as a central department store concierge desk.
   - Use the re-export syntax (`export * from ...`) to gather and re-export all symbols from `./userProfile` and `./orderHistory` in a single unified entrypoint.

4. **Section 4: The Consumer Service (`src/services/dashboardService.ts`)**
   - Import the domain symbols from the central barrel file `./models` (without specifying individual filenames).
   - Use strict **Type-Only Import syntax (`import type { ... }`)** for all type blueprints (`UserProfile`, `UserPermissions`, `OrderRecord`, `OrderStatus`) so the build bundler strips them instantly.
   - Use standard runtime import syntax for the runtime class `UserValidatorClass`. Demonstrate modern inline type import syntax (e.g., `import { UserValidatorClass, type UserProfile, type OrderRecord } from '../models';`).
   - Write a function `renderDashboardSummary(user: UserProfile, orders: OrderRecord[]): void` that validates the user's email at runtime using `UserValidatorClass` and logs a formatted summary.

5. **Section 5: Deep Technical Explanation**
   - Explain what happens to `import type` statements during the TypeScript compilation and bundling phase. How does this prevent server-side code bloat in client bundles?
   - Explain the "Barrel File Bloat" trap in massive monorepos. Why can importing one single helper from a root `index.ts` that re-exports 5,000 files slow down build times or cause circular dependency crashes?

---

## ANSWER HERE

### Section 1: Domain Model File 1 (`src/models/userProfile.ts`)

```typescript
// Write UserProfile interface, UserPermissions type, and UserValidatorClass here:
```

### Section 2: Domain Model File 2 (`src/models/orderHistory.ts`)

```typescript
// Write OrderRecord interface, OrderStatus type, and OrderProcessingEngine here:
```

### Section 3: The Central Barrel File (`src/models/index.ts`)

```typescript
// Write your clean re-export statements here:
```

### Section 4: The Consumer Service (`src/services/dashboardService.ts`)

```typescript
// Write your type-only imports and renderDashboardSummary function here:
```

### Section 5: Deep Technical Explanation

> **How `import type` prevents bundle bloat during compilation:**
> 

> **The Barrel File Bloat trap in enterprise monorepos:**
> 
