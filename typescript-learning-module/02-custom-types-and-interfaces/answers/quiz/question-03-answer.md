# Question 03 Answer

**Does `trainAnimal(dolphin)` error?**
No. It works perfectly.

**Why it works without `implements Swimmer`:**
TypeScript uses **structural typing**. It does not check whether `Dolphin` was formally declared as implementing `Swimmer`. It only checks whether the value being passed has all the properties that `Swimmer` requires. The `Swimmer` interface requires two things: a `swim()` method and a `speed: number`. The `Dolphin` class has both. Therefore TypeScript accepts it.

The class name `Dolphin` is irrelevant. All that matters is the shape of the object.

The extra `canEcholocate` property on `Dolphin` does not cause any problem. TypeScript only checks that the required properties are present. Extra properties are allowed.

**What would happen if `speed` was missing:**
TypeScript would produce an error like
```
Argument of type 'Dolphin' is not assignable to parameter of type 'Swimmer'.
Property 'speed' is missing in type 'Dolphin' but required in type 'Swimmer'.
```
