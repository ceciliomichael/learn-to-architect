# Module 19: Inheritance and Polymorphism

## Why this matters

Use inheritance only for a genuine substitutable is-a relationship.

## Contracts to learn

- **subtype:** A subtype must honor expectations established by its parent contract.
- **override:** @Override asks the compiler to verify that a method actually replaces an inherited method.
- **dynamic dispatch:** A call through a parent reference selects the runtime object's override.
- **final:** final can prevent unsafe extension or overriding.
- **composition first:** Prefer composition when behavior varies independently or the relationship is uses-a.

## Complete example

```java
public class Main {
    abstract static class Shape {
        abstract double area();
    }

    static final class Rectangle extends Shape {
        private final double width;
        private final double height;
        Rectangle(double width, double height) {
            if (width < 0 || height < 0) throw new IllegalArgumentException();
            this.width = width;
            this.height = height;
        }
        @Override double area() { return width * height; }
    }

    public static void main(String[] args) {
        Shape shape = new Rectangle(3, 4);
        System.out.println(shape.area());
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: 12.0.

## Deliberate practice

Add a Circle subtype and confirm one Shape method can use either implementation.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

Continue to [Module 20](../module-20-equality-hashing-and-ordering/README.md).

