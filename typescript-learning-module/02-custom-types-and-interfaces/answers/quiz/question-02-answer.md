# Question 02 Answer

**ShapeA  -  can you omit the property?**
Yes. `description?: string` marks the property as optional. The key does not need to appear in the object at all. `const a: ShapeA = {}` is completely valid.

**ShapeB  -  can you omit the property?**
No. `description: string | undefined` means the property is required to be present in the object, but its value is allowed to be `undefined`. You must write `const b: ShapeB = { description: undefined }`. Omitting the key entirely causes a TypeScript error: `Property 'description' is missing`.

**The key difference:**
- `property?: string`  -  The key itself is optional. It can be completely absent from the object.
- `property: string | undefined`  -  The key must exist in the object. The value can be `undefined`, but you cannot leave the key out.

In practice, `?` is almost always what you want when making a property optional. The explicit `| undefined` form is mainly useful when you want to force callers to consciously acknowledge the absence of a value.
