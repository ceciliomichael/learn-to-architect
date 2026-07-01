# Answer  -  Question 04: Generic Variance & Overload Order

## 1. Overload Order Rules
TypeScript evaluates overloaded function definitions sequentially from top to bottom, stopping at the very first signature whose parameter types match the call site arguments. If a broad signature (such as one accepting `any` or optional parameters) is placed first, TypeScript matches it immediately and ignores all subsequent, more precise generic signatures below it. Overloads must always be ordered from **most specific to least specific**.

## 2. Generic Type Inference Flow
When calling `parseConfig('{"port":"8080"}', (raw) => ({ port: Number(raw.port) }))`:
1. TypeScript inspects the second argument: arrow function `(raw) => ({ port: Number(raw.port) })`.
2. It evaluates the return expression `{ port: Number(raw.port) }` and infers the return type as `{ port: number }`.
3. It binds generic variable `T` to `{ port: number }`.
4. It sets the overall return type of `parseConfig` strictly to `{ port: number }`.

## 3. Separation of Overload Signatures vs Implementation Signature
The implementation signature (`function parseConfig(input: string, schema?: any): any`) is hidden from callers. It exists purely as the internal implementation bridge that satisfies all published overload contracts simultaneously. Because the implementation signature often uses loose types (`any` or optional parameters) to handle internal branching, exposing it to callers would destroy type safety. TypeScript restricts external callers exclusively to the published overload signatures above it.
