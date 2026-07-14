# Exercise solution

```java
public class Main {
    /**
     * Calculates a subtotal in integer cents.
     *
     * @param priceCents nonnegative price in cents
     * @param quantity nonnegative item count
     * @return exact subtotal in cents
     * @throws IllegalArgumentException when an input is negative
     * @throws ArithmeticException when multiplication overflows
     */
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

Treat public behavior and every installed dependency as maintained contracts rather than one-time setup. This reference solution preserves all lesson contracts and has this expected behavior: 375 and clean javadoc generation.

Complete the extension in small verified changes. Platform, timing, and external-service results must be recorded as environment-specific evidence rather than universal promises.

