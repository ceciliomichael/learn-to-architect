# Exercise solution

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

Use immutable values for stable facts and records for transparent data carriers. The program demonstrates each rule listed in the lesson and produces Product[name=Pen, priceCents=125] and 375.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

