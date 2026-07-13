# Question 04: for vs for...of

Explain the difference between a `for` loop and a `for...of` loop.

```typescript
const scores = [90, 75, 88];

// Loop A
for (let i = 0; i < scores.length; i++) {
  console.log(scores[i]);
}

// Loop B
for (let score of scores) {
  console.log(score);
}
```

1. What does `i` represent in Loop A that is not available in Loop B?
2. Both loops print the same output. When would you choose Loop A over Loop B?
3. When would Loop B be the better choice?

## ANSWER HERE

> **What `i` gives you that `for...of` does not:** `i` is the numeric array index. It lets the loop read or update an element by position and control the starting point, stopping condition, and step size.

> **When to choose Loop A (classic for):** Choose it when you need the index, need to skip positions, iterate backward, or otherwise control the counter precisely.

> **When to choose Loop B (for...of):** Choose it when you only need each value in sequence. It is simpler and avoids manual index bookkeeping.
