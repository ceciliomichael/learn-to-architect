# Challenge 02: Solution

```typescript
// Part 1: interface extends
interface Animal {
  name: string;
  age: number;
}

interface Bird extends Animal {
  wingspan: number;
  canFly: boolean;
}

const parrot: Bird = {
  name: "Polly",
  age: 5,
  wingspan: 0.4,
  canFly: true
};

// Part 2: type aliases with intersection (&)
type TypeAnimal = {
  name: string;
  age: number;
};

type TypeBird = TypeAnimal & {
  wingspan: number;
  canFly: boolean;
};

const eagle: TypeBird = {
  name: "Bald Eagle",
  age: 8,
  wingspan: 2.1,
  canFly: true
};
```

Both approaches produce identical types. The `extends` keyword on interfaces and the `&` intersection on type aliases achieve the same structural result. Most teams use `interface extends` for object shapes because it reads more clearly.
