# Question 01 Answer

**Union  -  can you access `val.name` directly?**
No. `UnionAB` means `val` is either an `A` (which has `name`) OR a `B` (which has `age` but no `name`). TypeScript cannot guarantee that `name` exists because `val` might be a `B`. Accessing `val.name` directly is a compile error. You must narrow first with `if ("name" in val)`.

**Intersection  -  can you access `val2.name` directly?**
Yes. `IntersectionAB` means `val2` must have ALL properties from both `A` and `B`. It is guaranteed to have both `name` and `age`. You can access either without any check.

**Real-world analogy for union:**
A vehicle that is either a car OR a motorcycle  -  you cannot assume it has four wheels without checking which one it is.

**Real-world analogy for intersection:**
A swimming cyclist who is both a swimmer AND a cyclist simultaneously  -  they have every skill from both categories with no need to check.
