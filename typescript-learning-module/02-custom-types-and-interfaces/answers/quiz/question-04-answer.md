# Question 04 Answer: Type Aliases vs Interfaces Capabilities

## 1. Core Answer & Explanation

While both `interface` and `type` can describe object structures, they represent different concepts in TypeScript's grammar: an **Interface** is a formal structural blueprint specifically for object shapes, whereas a **Type Alias** is an immutable binding name for *any* arbitrary type expression.

### 1. What Only `type` Can Do (Type-Only Superpowers)
A `type` alias can assign a name to non-object type expressions. Specifically, only `type` can represent:
* **Primitive Aliases:** Nicknames for built-in primitives (`type ID = string;`).
* **Union Types:** An expression requiring a value to match one of several types (`type Status = "pending" | "success" | "error";`).
* **Tuple Types:** Fixed-length array structures with specific positional types (`type Coordinate = [number, number, string];`).
* **Conditional & Mapped Types:** Advanced functional type transformations (`type Readonly<T> = { readonly [P in keyof T]: T[P] };`).

An interface **cannot** model primitives, unions, or tuples directly. Attempting to write `interface Status = "pending" | "success";` results in a fatal syntax error.

### 2. What Only `interface` Can Do (Interface-Only Superpowers)
* **Declaration Merging:** As explored in Question 01, declaring two interfaces with the same name merges their properties into a unified contract. Doing this with `type` throws a `Duplicate identifier` error.
* **Hierarchy Caching & Faster Compilation:** When an interface extends another interface (`interface B extends A`), TypeScript caches the structural relationship by name, resulting in faster compilation and cleaner IDE error tooltips.

---

## 2. Complete Code Examples & Syntax Comparison

```typescript
// ==========================================
// What ONLY Type Aliases Can Do
// ==========================================

// 1. Union Types
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE";

// 2. Tuple Types (Positional Arrays)
type DatabaseRow = [id: number, username: string, isAdmin: boolean];

// 3. Primitive Aliases
type UUID = string;

// 4. Composing Unions with Object Shapes
type APIResponse = 
  | { status: "success"; data: string[] }
  | { status: "error"; errorMessage: string };

// Attempting to write any of the above using 'interface' is a SYNTAX ERROR:
// interface HttpMethod = "GET" | "POST"; // ERROR: '=' is not allowed in interface declaration!


// ==========================================
// What ONLY Interfaces Can Do
// ==========================================

// 1. Declaration Merging
interface GlobalLogger {
  log(msg: string): void;
}
interface GlobalLogger {
  error(msg: string): void;
}
// Both methods are now required on GlobalLogger!
```

---

## 3. Symbol-by-Symbol Breakdown

* `type HttpMethod = ...` -> The `type` keyword functions like `const` or `let` in variable declarations: it binds an identifier (`HttpMethod`) to an expression on the right side of the assignment operator (`=`).
* `"GET" | "POST"` -> String literal types combined via the union operator `|`.
* `[id: number, ...]` -> Square brackets in a type position define a **Tuple**. The optional labels (`id:`) provide documentation in IDE tooltips without altering the underlying array indexing rules.
* `interface GlobalLogger { ... }` -> Notice the **complete absence of an equals sign (`=`)** between the identifier and the opening curly brace `{`. An interface is a declarative statement, not an assignment expression!

---

## 4. Senior Engineer's Decision Matrix

In enterprise software engineering, choosing between `interface` and `type` should never be a matter of personal styling whim; it should follow a strict, standardized decision matrix across your organization:

| Architectural Requirement | Recommended Keyword | Technical Rationale |
| :--- | :--- | :--- |
| **Domain Models & Object Shapes** (Users, Orders, Products, Database Entities) | **`interface`** | Provides clean hierarchical inheritance via `extends`, superior compiler performance through name caching, and highly readable compiler error messages that reference the interface name rather than expanding raw object literals. |
| **Public Open-Source Libraries & SDKs** | **`interface`** | Essential for third-party consumers who may need to augment or extend your configuration options via Declaration Merging (e.g., adding custom plugins to an SDK configuration). |
| **State Transitions & Discriminated Unions** (Redux Actions, API Responses, UI States) | **`type`** | Interfaces physically cannot model union expressions (`ActionA \| ActionB`). Type aliases allow building exhaustive, type-safe state machines using discriminated unions. |
| **Primitive Nicknames & Tuples** (IDs, Coordinates, Fixed Arrays) | **`type`** | Required by TypeScript grammar; interfaces cannot model non-object structures. |
| **Advanced Type Transformations** (Mapped Types, Conditional Types, Generics) | **`type`** | Functional type manipulation (such as extracting keys with `keyof`, filtering properties, or creating utility types) requires type alias expressions. |

### Summary Rule for Production Teams
> **"Use `interface` until you need a feature that only `type` provides."**
> Start by defining all standard object blueprints and class contracts as `interface`. Immediately reach for `type` whenever you need unions, tuples, primitive aliases, or complex functional type transformations.
