# Exercise solution

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

Define value identity consistently before using custom objects as collection keys. This solution enforces the lesson contracts and has the expected behavior: products ordered by price, then true.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

