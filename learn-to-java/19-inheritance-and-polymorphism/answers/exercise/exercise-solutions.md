# Exercise solution

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

Use inheritance only for a genuine substitutable is-a relationship. This solution enforces the lesson contracts and has the expected behavior: 12.0.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

