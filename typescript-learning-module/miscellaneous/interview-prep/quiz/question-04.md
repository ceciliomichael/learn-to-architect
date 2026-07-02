# Question 04: Generic Variance & Overload Order

An interviewer shows you the following generic data pipeline helper
```typescript
function parseConfig(input: string): Record<string, string>;
function parseConfig<T>(input: string, schema: (raw: Record<string, string>) => T): T;
function parseConfig(input: string, schema?: any): any {
  const raw = JSON.parse(input);
  return schema ? schema(raw) : raw;
}
```

1. Why does TypeScript require function overloads to be ordered from most specific to least specific? What happens if an overload signature accepting `any` or optional parameters is placed first?
2. When calling `parseConfig('{"port":"8080"}', (raw) => ({ port: Number(raw.port) }))`, how does TypeScript infer generic type `T` from the callback's return signature?
3. What is the architectural benefit of separating overload signatures from the implementation signature? Why can callers never invoke the implementation signature directly?

## ANSWER HERE

> **1. Overload order rules:**

> **2. Generic type inference flow:**

> **3. Separation of overload signatures vs implementation signature:**
