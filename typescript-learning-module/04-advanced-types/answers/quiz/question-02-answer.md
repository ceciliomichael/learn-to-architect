# Question 02 Answer

```typescript
interface VideoFile { duration: number; codec: string; }
interface ImageFile { width: number; height: number; }

function describeMedia(file: VideoFile | ImageFile): string {
  if ("duration" in file) {
    // TypeScript narrows 'file' to VideoFile here:
    return `Video: ${file.duration}s, codec: ${file.codec}`;
  } else {
    // TypeScript narrows 'file' to ImageFile here:
    return `Image: ${file.width}x${file.height}`;
  }
}
```

**How the `in` operator works for narrowing:**
The `in` operator checks whether a specific property name exists on an object at runtime. When you write `"duration" in file`, JavaScript checks if the object currently stored in `file` has a property called `duration`.

TypeScript understands this check. Because `duration` only exists on `VideoFile` and not on `ImageFile`, TypeScript narrows the type inside the `if` block to `VideoFile`. In the `else` block, since TypeScript knows `duration` is not present, it narrows to `ImageFile`.

This is useful when two interface types share no common unique property that you can check with `typeof`.
