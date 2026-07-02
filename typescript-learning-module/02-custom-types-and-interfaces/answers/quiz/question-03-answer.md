# Question 03: Answer

1. **Does assigning point3D to point produce an error?**
No, it does not produce an error.

2. **Why TypeScript allows extra properties:**
TypeScript uses **structural typing** (duck typing). When checking if `point3D` satisfies the `Point2D` interface, the compiler only verifies that `point3D` has at least the required properties (`x: number` and `y: number`). Even though `point3D` has an extra property (`z: number`), it still possesses all the structure required by `Point2D`, so TypeScript accepts the assignment.

3. **What happens if property y is missing:**
TypeScript will throw a compile-time error: `Property 'y' is missing in type '{ x: number; z: number; }' but required in type 'Point2D'`. Structural typing requires that all mandatory properties defined in the blueprint must be present.
