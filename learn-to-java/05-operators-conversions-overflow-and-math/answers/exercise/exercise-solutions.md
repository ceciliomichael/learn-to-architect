# Exercise solution

```java
public class Main {
    public static void main(String[] args) {
        int priceCents = 125;
        int quantity = 3;
        int subtotal = Math.multiplyExact(priceCents, quantity);
        double average = (double) subtotal / quantity;
        System.out.printf("%d %.2f%n", subtotal, average);
    }
}
```

Calculate deliberately while recognizing integer division, narrowing, and overflow. The program demonstrates each rule listed in the lesson and produces 375 125.00.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

