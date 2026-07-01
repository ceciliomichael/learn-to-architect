# Question 01 Answer

**What is a callback?**
A callback is a function that you pass as an argument to another function. The receiving function calls your function at some point during its own execution.

**The callback in the code is:**
`(num) => num * 2`  -  the arrow function passed to `.map()`.

**How TypeScript knows `num` is a number:**
This is called **contextual typing**. Because `.map()` is called on `[1, 2, 3]` (which TypeScript knows is a `number[]`), TypeScript can infer that the callback will receive each item one at a time, and each item is a `number`. So TypeScript automatically assigns `num` the type `number` without you needing to write it explicitly.

**What happens if you call `num.toUpperCase()`:**
TypeScript throws a compile error: `Property 'toUpperCase' does not exist on type 'number'`. Since TypeScript knows `num` is a number, and numbers do not have a `.toUpperCase()` method, it blocks the call immediately  -  before the code ever runs.
