# Question 04 Answer

**What `i` gives you that `for...of` does not:**
`i` is the index  -  the numerical position of the current item in the array. Inside `for...of`, you only get the value of each item. You do not get its position.

**When to choose Loop A (classic `for` loop):**
- When you need the index of each item (e.g. "print Item 1: ..., Item 2: ...").
- When you need to loop backward (decrement `i`).
- When you need to skip items or step by more than one (`i += 2`).
- When you are modifying the array while iterating (rare but sometimes needed).

**When to choose Loop B (`for...of`):**
- When you only care about the values, not their positions.
- When the loop body is straightforward and readable clarity matters.
- When iterating over items to log them, transform them, or accumulate a result.

In practice, `for...of` is the more common and readable choice for most array iteration. Use the classic `for` loop only when you specifically need the index or need fine-grained control over the iteration step.
