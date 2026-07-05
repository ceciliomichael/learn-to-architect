# Question 01 Answer: Callbacks and Contextual Typing

This document provides an exhaustive architectural analysis, compiler mechanics breakdown, and symbol-by-symbol clarity for **Question 01: Callbacks and Contextual Typing**.

---

## 1. Complete Conceptual Answers

### What is a callback function? Identify the callback in the line above.
A **callback function** is an executable function that is passed as an argument into another function or method. The receiving function (often called the higher-order function or host function) stores the reference to the callback and executes it at an appropriate moment during its own workflow.

In the provided line of code:
```typescript
const doubled = [1, 2, 3].map((num) => num * 2);
```
The callback function is the inline arrow function expression: **`(num) => num * 2`**.

### How does TypeScript know `num` is a `number` without an explicit annotation?
This mechanism is known as **Contextual Typing** (or bidirectional type inference). 
When you call `.map()` on an array literal `[1, 2, 3]`, the TypeScript type checker first determines the type of the source array: `number[]` (an array of numbers). 
The built-in type definition for `Array<T>.prototype.map()` states that its callback parameter must accept an argument of type `T`. Because `T` is locked down as `number`, the compiler flows this type information *backward* into the inline callback expression. Consequently, TypeScript automatically assigns the type `number` to the parameter `num` without requiring the developer to write `(num: number)`.

### What happens if you call `num.toUpperCase()` inside the callback?
TypeScript immediately throws a **compile-time error**:
`Property 'toUpperCase' does not exist on type 'number'.`
Because Contextual Typing has already proven that `num` is strictly a numeric primitive, the type checker inspects the prototype of `Number`. Since `.toUpperCase()` is a string method that does not exist on numbers, TypeScript blocks the compilation before any code is ever transpiled or executed in JavaScript.

---

## 2. Symbol-by-Symbol Analysis

Let us deconstruct the expression `[1, 2, 3].map((num) => num * 2)`:
* `[` and `]`: Array literal syntax defining a standard JavaScript array containing three numbers.
* `.map`: Member access operator invoking the standard array transformation method.
* `(` (after map): Opening parenthesis marking the argument list of the `.map()` method call.
* `(` and `)` (around num): Parentheses enclosing the input parameter list of our inline arrow function callback.
* `num`: Developer-assigned parameter identifier representing the current numerical element being processed.
* `=>`: Fat arrow syntax defining an arrow function expression. It separates parameter requirements from the calculation body.
* `num * 2`: Mathematical calculation expression. Because curly braces `{}` are omitted, this is an **implicit return expression**.
* `)` (final): Closing parenthesis terminating the `.map()` method invocation.

---

## 3. Architectural Trade-Offs and Best Practices

### Contextual Typing vs. Explicit Callback Annotations
Beginners often ask: *Should I explicitly write `(num: number) => num * 2` to be safe?*
In enterprise TypeScript engineering, **leveraging Contextual Typing for inline callbacks is the recommended best practice**. Writing redundant type annotations on inline callbacks clutters code readability without adding type safety. 
However, there is an important architectural boundary: **if a callback is declared as a standalone function outside the call site, explicit type annotations are mandatory**:
```typescript
// Good: Contextual typing handles inline callback cleanly
const inlineResult = [1, 2, 3].map((num) => num * 2);

// Good: Standalone callback requires explicit type annotations!
const doubleHandler = (num: number): number => num * 2;
const standaloneResult = [1, 2, 3].map(doubleHandler);
```
Without explicit annotations on `doubleHandler`, TypeScript would evaluate `num` in isolation, defaulting to an implicit `any` error under strict mode!
