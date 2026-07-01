# Challenge 03: Solution

```typescript
interface Printable {
  print(): void;
}

abstract class Shape implements Printable {
  abstract getArea(): number;
  abstract print(): void;

  describe(): void {
    console.log("This shape has an area of " + this.getArea());
  }
}

class Circle extends Shape {
  constructor(public radius: number) {
    super();
  }

  getArea(): number {
    return 3.14159 * this.radius * this.radius;
  }

  print(): void {
    console.log("Drawing a circle with radius " + this.radius);
  }
}

class Rectangle extends Shape {
  constructor(public width: number, public height: number) {
    super();
  }

  getArea(): number {
    return this.width * this.height;
  }

  print(): void {
    console.log("Drawing a rectangle " + this.width + "x" + this.height);
  }
}

const circle = new Circle(5);
circle.describe(); // "This shape has an area of 78.53975"
circle.print();    // "Drawing a circle with radius 5"

const rect = new Rectangle(8, 3);
rect.describe();   // "This shape has an area of 24"
rect.print();      // "Drawing a rectangle 8x3"

// new Shape();
// ERROR: Cannot create an instance of an abstract class.
```
