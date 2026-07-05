# Challenge 03: Advanced Type Manipulation Engines

Practice building custom type transformers from scratch using Mapped Types (`[P in keyof T]`), routing types dynamically with Conditional Types (`T extends U ? X : Y`) and `infer`, and enforcing string patterns with Template Literal Types (`${string}`).

## Your Tasks

**Part 1: Mapped Type Transformers**
1. Write a custom generic Mapped Type called `NullableProperties<T>`. Inside the type definition, loop over every property `P` in `keyof T` and transform its value type to `T[P] | null`.
2. Given the interface below, apply your custom transformer to create a type alias `NullableServerConfig`:
```typescript
interface ServerConfig {
  hostname: string;
  port: number;
  enableSsl: boolean;
}
```
3. Create a valid test object `testConfig: NullableServerConfig` where every property is explicitly assigned `null`.

**Part 2: Conditional Types and the `infer` Keyword**
4. Write a generic Conditional Type called `UnwrapPromise<T>`. If type `T` is assignable to `Promise<infer ResultType>`, extract and return `ResultType`. Otherwise, return `T` unchanged.
5. Test your conditional type by creating:
   - `type StringResult = UnwrapPromise<Promise<string>>;` (Should resolve to `string`)
   - `type NumberResult = UnwrapPromise<number>;` (Should resolve to `number`)

**Part 3: Template Literal Types**
6. Create a type alias `WarehouseSku` that enforces a strict formatting pattern: strictly the prefix `"SKU-"`, followed by a `number`, followed by a hyphen and a `string` (e.g., `"SKU-100-MONITOR"`).
7. Create an entity union `type Resource = "user" | "document" | "report";` and an action union `type Action = "create" | "read" | "update" | "delete";`. Use Template Literal interpolation (`${Resource}:${Action}`) to generate a combined type alias `ResourcePermission` containing all 12 possible permission strings.
8. Declare a variable `myPermission: ResourcePermission = "document:update";` and verify that TypeScript compiles without errors.

## ANSWER HERE

```typescript
// Part 1: Mapped Type Transformers
interface ServerConfig {
  hostname: string;
  port: number;
  enableSsl: boolean;
}

// Write NullableProperties<T>, NullableServerConfig, and testConfig here:



// Part 2: Conditional Types and infer
// Write UnwrapPromise<T>, StringResult, and NumberResult here:



// Part 3: Template Literal Types
type Resource = "user" | "document" | "report";
type Action = "create" | "read" | "update" | "delete";

// Write WarehouseSku, ResourcePermission, and test variables here:



```
