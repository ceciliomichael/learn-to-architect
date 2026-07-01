# Question 03: Parameter Property Shorthand

Rewrite the following class using TypeScript's parameter property shorthand so that the class has zero lines inside the constructor body and zero separate property declarations above it:

```typescript
class Point {
  public x: number;
  public y: number;
  readonly label: string;
  private createdAt: Date;

  constructor(x: number, y: number, label: string) {
    this.x = x;
    this.y = y;
    this.label = label;
    this.createdAt = new Date();
  }
}
```

Note: `createdAt` is assigned to `new Date()` inside the constructor (not directly from a parameter). For that property, you cannot use parameter shorthand  -  keep the assignment inside the body.

## ANSWER HERE

```typescript
// Rewrite Point using parameter property shorthand:
class Point {

}
```
