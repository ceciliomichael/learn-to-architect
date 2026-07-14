# Exercise solution

```java
public class Main {
    static int subtotal(int priceCents, int quantity) {
        if (priceCents < 0 || quantity < 0) {
            throw new IllegalArgumentException("values must be nonnegative");
        }
        return Math.multiplyExact(priceCents, quantity);
    }

    public static void main(String[] args) {
        System.out.println(subtotal(125, 3));
    }
}
```

Give one focused behavior a name, explicit inputs, and a checked output contract. The program demonstrates each rule listed in the lesson and produces 375.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

