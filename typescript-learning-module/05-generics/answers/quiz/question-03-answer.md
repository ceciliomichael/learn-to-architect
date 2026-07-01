# Question 03 Answer

**Difference between `[string, number]` and `(string | number)[]`:**
`[string, number]` is a tuple: a fixed-length array where the type at each specific position is defined. Position 0 must be a string, position 1 must be a number, and the array can only have exactly 2 items.

`(string | number)[]` is a regular array of any length where each item can be either a string or a number, in any order. There is no constraint on length or position.

**Error when order is wrong:**
```
Type '[number, string]' is not assignable to type '[string, number]'.
Type 'number' is not assignable to type 'string'.
```
TypeScript checks each position individually.

**Real-world scenario for a tuple:**
A function that returns coordinates `[latitude, longitude]`  -  both are numbers, the order matters (lat first, lon second), and you always expect exactly two values. A tuple `[number, number]` expresses this more precisely than an interface and avoids needing to name the properties.

Another common example: the return value of `useState` in React, which is typed as `[State, SetState]`  -  a tuple with exactly two items where position determines meaning.
