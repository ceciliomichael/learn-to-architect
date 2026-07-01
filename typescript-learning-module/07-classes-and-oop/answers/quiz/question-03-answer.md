# Question 03 Answer

```typescript
class Point {
  private createdAt: Date;

  constructor(
    public x: number,
    public y: number,
    readonly label: string
  ) {
    // 'x', 'y', and 'label' are automatically declared and assigned by the shorthand above.
    // 'createdAt' cannot use shorthand because its value is not a constructor parameter.
    this.createdAt = new Date();
  }
}
```

The parameter property shorthand works for any constructor parameter that should be directly stored as a class property with the same name. You just prefix the parameter with an access modifier (`public`, `private`, `protected`) or `readonly`. TypeScript automatically generates the property declaration and the `this.x = x` assignment for you.

Properties whose values are computed from something other than a constructor parameter (like `new Date()`) must still be initialized manually inside the constructor body.
