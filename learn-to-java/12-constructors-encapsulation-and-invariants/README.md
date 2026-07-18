# Module 12: Constructors, Encapsulation, and Invariants

## Why this matters

Prevent invalid object states by validating construction and controlling mutation.

## Rules to learn

- **constructor:** A constructor initializes a new object and has no return type.
- **private fields:** Private fields prevent unrelated code from changing state directly.
- **invariant:** An invariant is a rule every observable object state must satisfy.
- **validation:** Reject invalid constructor and method inputs before changing fields.
- **accessor:** An accessor exposes only the information callers need.

## Complete example

```java
public class Main {
    static final class Product {
        private final String name;
        private int priceCents;

        Product(String name, int priceCents) {
            if (name == null || name.isBlank() || priceCents < 0) {
                throw new IllegalArgumentException("invalid product");
            }
            this.name = name.strip();
            this.priceCents = priceCents;
        }

        String name() { return name; }
        int priceCents() { return priceCents; }
        void changePrice(int value) {
            if (value < 0) throw new IllegalArgumentException("negative price");
            priceCents = value;
        }
    }

    public static void main(String[] args) {
        Product product = new Product(" Pen ", 125);
        product.changePrice(150);
        System.out.println(product.name() + " " + product.priceCents());
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: Pen 150.

## Deliberate practice

Attempt invalid construction and verify the existing valid product remains unchanged.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 13](../13-immutability-and-records/README.md).
