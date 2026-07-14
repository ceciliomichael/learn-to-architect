# Module 30 Exercise Solutions

```typescript
type PrimitiveName<T> = T extends string ? "text" : "other";

type BoxEach<T> = T extends unknown ? { value: T } : never;
type DistributedBox = BoxEach<string | number>;

type KeepNumbers<T> = T extends number ? T : never;
type Numeric = KeepNumbers<string | 1 | 2 | boolean>;

type ArrayItem<T> = T extends readonly (infer Item)[] ? Item : never;
type TextItem = ArrayItem<readonly string[]>;
type NotAnItem = ArrayItem<number>;

type IdType<T> = T extends { id: infer Id } ? Id : never;
```

`DistributedBox` is `{ value: string } | { value: number }`. `Numeric` is `1 | 2`. `NotAnItem` is `never`.
