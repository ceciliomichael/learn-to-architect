# Module 13: Immutability and Records

## Why this matters

Use immutable values for stable facts and records for transparent data carriers.

## Rules to learn

- **immutable state:** An immutable type does not expose a state change after construction.
- **defensive copy:** Mutable arrays and collections need copying at immutable boundaries.
- **record:** A record supplies final components, accessors, equality, hashing, and a readable toString.
- **compact constructor:** A record compact constructor can validate and normalize components.
- **with behavior:** A record may contain methods, but its components still describe its state.

## Complete example

```java
public class Main {
    record Product(String name, int priceCents) {
        Product {
            if (name == null || name.isBlank() || priceCents < 0) {
                throw new IllegalArgumentException("invalid product");
            }
            name = name.strip();
        }

        int subtotal(int quantity) {
            if (quantity < 0) throw new IllegalArgumentException("quantity");
            return Math.multiplyExact(priceCents, quantity);
        }
    }

    public static void main(String[] args) {
        Product product = new Product(" Pen ", 125);
        System.out.println(product);
        System.out.println(product.subtotal(3));
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: Product[name=Pen, priceCents=125] and 375.

## Deliberate practice

Create two equal records and confirm equals and hashCode agree.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 14](../14-enums-sealed-types-and-pattern-matching/README.md).
