# Question 05: Advanced Type Engines

Mastering TypeScript requires understanding its advanced type computation engines: Mapped Types (`[P in keyof T]`), Conditional Types (`T extends U ? X : Y`), and Template Literal Types (`${string}`). This question tests your architectural understanding of how these engines operate.

```typescript
// Example A: Mapped Type
type ReadonlyOptional<T> = {
  readonly [P in keyof T]?: T[P];
};

// Example B: Conditional Type with infer
type ExtractArrayElement<T> = T extends Array<infer E> ? E : T;

// Example C: Template Literal Type
type EventName<Entity extends string, Action extends string> = `${Entity}:${Action}`;
```

## Questions

1. **Mapped Type Assembly Mechanics**:
   - In Example A, explain the exact purpose of every symbol: `[ ]`, `P`, `in`, `keyof T`, `readonly`, `?`, and `T[P]`.
   - How does `ReadonlyOptional<T>` transform an interface like `{ name: string; age: number; }`?
2. **Conditional Types and the `infer` Keyword**:
   - In Example B, explain how the ternary syntax (`condition ? trueType : falseType`) routes types during compilation.
   - What is the exact pedagogical purpose of the `infer` keyword in `Array<infer E>`? What happens if you pass `string[]` versus `boolean` into `ExtractArrayElement<T>`?
3. **Template Literal Pattern Enforcement**:
   - In Example C, if you pass `Entity = "user" | "order"` and `Action = "created" | "deleted"`, how does TypeScript compute the resulting type?
   - Why is generating string unions at the type level superior to writing magic string constants in event-handling functions?

## ANSWER HERE

> **1. Mapped Type Assembly Mechanics:**

> **2. Conditional Types and the `infer` Keyword:**

> **3. Template Literal Pattern Enforcement:**
