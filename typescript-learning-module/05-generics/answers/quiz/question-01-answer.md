# Question 01 Answer

**Type of `result1` and what happens with `.toFixed(2)`:**
`result1` is typed as `any`. TypeScript allows calling `.toFixed(2)` on it without error  -  even though strings do not have `.toFixed()`. The code compiles, but crashes at runtime with: `result1.toFixed is not a function`.

**Type of `result2` and what happens with `.toFixed(2)`:**
`result2` is typed as `string` (TypeScript inferred `T = string` from the `"hello"` argument). Calling `result2.toFixed(2)` produces a compile-time error: `Property 'toFixed' does not exist on type 'string'`. TypeScript catches this before the code ever runs.

**What `<T>` does:**
A generic type variable `<T>` is a placeholder that TypeScript fills in with the actual type at the call site, allowing one function to work safely across many types while preserving the specific type information throughout.
