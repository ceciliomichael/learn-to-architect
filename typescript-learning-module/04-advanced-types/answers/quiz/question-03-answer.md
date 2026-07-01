# Question 03 Answer

**Inside if-block with Version A:**
TypeScript still treats `pet` as `Cat | Dog`. A plain `boolean` return tells TypeScript nothing about what the result means for the type. Inside `if (isCat(pet))`, the variable `pet` remains the full union type and you cannot call cat-specific methods without another check.

**Inside if-block with Version B:**
TypeScript narrows `pet` to exactly `Cat`. The type predicate `pet is Cat` is a special instruction to the compiler: "If this function returns `true`, treat `pet` as `Cat` from this point on." Inside the `if` block, you have full access to all `Cat` properties and methods without any further checks.

**What `pet is Cat` tells the compiler:**
A type predicate tells the compiler the relationship between the boolean return value and the type of a specific parameter. Plain `boolean` only says "yes or no." `pet is Cat` says "if yes, then `pet` is definitely a `Cat`." This is the extra semantic meaning that makes narrowing possible.
