# Question 01: Callbacks and Contextual Typing

Look at this line
```typescript
const doubled = [1, 2, 3].map((num) => num * 2);
```

1. What is a "callback function"? Identify the callback in the line above.
2. The parameter `num` has no type annotation. How does TypeScript know `num` is a `number` without you writing `(num: number)`?
3. What would happen if you tried to call `num.toUpperCase()` inside the callback? Why?

## ANSWER HERE

> **What is a callback?:** A callback is a function passed to another function so that the receiving function can invoke it. Here, `.map()` invokes the callback once for each array element.

> **The callback in the code above is:** `(num) => num * 2`.

> **How TypeScript knows num is a number:** The source array contains numbers, and the type signature of `.map()` contextually types its callback parameter as the array element type. Therefore, `num` is inferred as `number`.

> **What happens if you call num.toUpperCase():** TypeScript reports an error because `toUpperCase()` is a string method and does not exist on `number`.
