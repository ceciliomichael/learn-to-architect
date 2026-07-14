# Module 20: Equality, Hashing, and Ordering

## Why this matters

Define value identity consistently before using custom objects as collection keys.

## Contracts to learn

- **equals:** equals should be reflexive, symmetric, transitive, consistent, and false for null.
- **hashCode:** Equal objects must return equal hash codes.
- **record equality:** Records generate component-based equals and hashCode.
- **Comparable:** Comparable defines one natural ordering and must agree with its documented equality policy.
- **Comparator:** A Comparator supplies an explicit alternative ordering.

## Complete example

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class Main {
    record Product(String name, int priceCents) {}

    public static void main(String[] args) {
        List<Product> products = new ArrayList<>(List.of(
                new Product("Book", 1200),
                new Product("Pen", 125)));
        products.sort(Comparator.comparingInt(Product::priceCents));
        System.out.println(products);
        System.out.println(new Product("Pen", 125).equals(new Product("Pen", 125)));
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: products ordered by price, then true.

## Deliberate practice

Add a name comparator without changing the record's equality.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

Continue to [Module 21](../module-21-lambdas-and-functional-interfaces/README.md).

