# Question 03 Answer: Rest Parameter Type

This document provides an exhaustive architectural analysis, compiler mechanics breakdown, and symbol-by-symbol clarity for **Question 03: Rest Parameter Type**.

---

## 1. Complete Conceptual Answers

### Which option is correct and why?
**The correct option is B: `...words: string[]`** (or alternatively written using generic syntax as `...words: Array<string>`).

When you declare a rest parameter in TypeScript using three consecutive periods (`...`), you are instructing the JavaScript runtime engine to gather all remaining individual arguments passed by the caller and bundle them into a single, unified Array container inside the function body. 
Because the arguments are physically gathered into an array instance at runtime, **the TypeScript type annotation for a rest parameter must always be an array type**. Writing `string[]` explicitly informs the compiler: *"This parameter will collect zero or more individual string arguments and present them to my code as an array of strings."*

### Why the other options fail at compile time
* **Option A (`...words: string`)**: Incorrect. This omits the array brackets `[]`. In TypeScript syntax rules, annotating a rest parameter with a non-array primitive type (`string`, `number`, `boolean`) causes an immediate syntax error: `A rest parameter must be of an array type.`
* **Option C (`words: ...string`)**: Incorrect. In JavaScript and TypeScript grammar, the three-period rest operator `...` must prefix the parameter identifier (`...words`), never the type annotation (`...string`).
* **Option D (`words: Array`)**: Incorrect. While `Array` is a valid generic interface name, writing `Array` without a generic type argument (`<string>`) is incomplete syntax in TypeScript and causes a compile error: `Generic type 'Array<T>' requires 1 type argument(s).` Furthermore, it is missing the mandatory `...` rest prefix on the parameter name!

### What type does `words` have inside the function body?
Inside the executable body of the `shout` function, the parameter `words` has the exact type **`string[]`** (an array of strings).
You can safely perform all standard array operations on it without type assertions:
```typescript
function shout(...words: string[]): string {
  console.log("Word count:", words.length); // .length is available on string[]
  
  // We can iterate over string[] using for...of or call array methods like .map() and .join()
  return words.map((w) => w.toUpperCase()).join(" ");
}
```

---

## 2. Symbol-by-Symbol Analysis

Let us deconstruct the parameter definition `...words: string[]`:
* `...` (Three periods): The built-in **Rest Parameter Operator**. In the AST, this marks the parameter as variadic, instructing the runtime engine to collect all trailing arguments passed at call site.
* `words`: Developer-assigned parameter identifier representing the bundled array container inside the function scope.
* `:`: Type annotation anchor binding the parameter to its type rule.
* `string`: The required primitive type for every individual argument passed into the variadic slot.
* `[]`: Array type syntax. Combined with `string`, this forms `string[]`, satisfying the compiler's strict requirement that all rest parameters evaluate to array types.

---

## 3. Architectural Trade-Offs and Best Practices

### Variadic Rest Parameters vs. Standard Array Arguments
When designing enterprise APIs, senior architects must choose between variadic rest parameters (`...words: string[]`) and standard array parameters (`words: string[]` without `...`).
* **Use Rest Parameters** when building utility functions, loggers, or math accumulators where requiring callers to instantiate array literals adds unnecessary friction:
  ```typescript
  // Ergonomic call site using rest parameters
  shout("Hello", "from", "TypeScript");
  ```
* **Use Standard Array Parameters** when the data being passed already exists as a collection in the caller's scope, or when the function needs to accept multiple distinct collections as inputs (remember: a function can only have one rest parameter, and it must appear at the very end of the signature!).
