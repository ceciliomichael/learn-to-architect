# Question 03: Structural Typing

TypeScript uses structural typing (shape-based compatibility). Consider this
```typescript
interface Swimmer {
  swim(): void;
  speed: number;
}

class Dolphin {
  swim(): void {
    console.log("Splashing around.");
  }
  speed: number = 40;
  canEcholocate: boolean = true;
}

function trainAnimal(animal: Swimmer): void {
  animal.swim();
}

const dolphin = new Dolphin();
trainAnimal(dolphin);
```

1. Does `trainAnimal(dolphin)` produce a TypeScript error? Why or why not?
2. `Dolphin` was never declared as `implements Swimmer`. Why does it still work?
3. What would happen if `Dolphin` was missing the `speed` property?

## ANSWER HERE

> **Does it error?**

> **Why it works without `implements Swimmer`:**

> **What happens if speed is missing:**
