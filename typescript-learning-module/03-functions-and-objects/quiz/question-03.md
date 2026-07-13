# Question 03: Rest Parameter Type

What is the correct TypeScript type annotation for a rest parameter that accepts any number of strings?

```typescript
function shout(...words: ???): string {
  return words.join(" ").toUpperCase();
}
```

**Options:**

A) `...words: string`

B) `...words: string[]`

C) `words: ...string`

D) `words: Array`

---

Which is correct and why? What type does `words` have inside the function body?

## ANSWER HERE

> **My choice:** B.

> **Why:** A rest parameter gathers all remaining arguments into an array, so a rest parameter accepting strings must be annotated as `string[]`.

> **Type of `words` inside the function:** Its type is a string[].
