# Question 02: The `in` Operator

What is the `in` operator and how is it used for type narrowing?

Write a concrete example using two interfaces that each have a unique property
```typescript
interface VideoFile { duration: number; codec: string; }
interface ImageFile { width: number; height: number; }

function describeMedia(file: VideoFile | ImageFile): string {
  // Use 'in' to narrow here
}
```

Complete the function body using the `in` operator to narrow the type, then explain in your answer how `in` works.

## ANSWER HERE

```typescript
function describeMedia(file: VideoFile | ImageFile): string {
  // Write your in-based narrowing here
}
```

> **How the `in` operator works for narrowing:**
