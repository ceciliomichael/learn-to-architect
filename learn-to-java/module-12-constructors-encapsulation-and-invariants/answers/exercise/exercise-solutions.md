# Exercise solution

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

Prevent invalid object states by validating construction and controlling mutation. The program demonstrates each rule listed in the lesson and produces Pen 150.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

