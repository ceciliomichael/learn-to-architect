# Exercise solution

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertThrows;

import org.junit.jupiter.api.Test;

class PriceTest {
    static int subtotal(int price, int quantity) {
        if (price < 0 || quantity < 0) throw new IllegalArgumentException();
        return Math.multiplyExact(price, quantity);
    }

    @Test
    void calculatesSubtotal() {
        assertEquals(375, subtotal(125, 3));
    }

    @Test
    void rejectsNegativeQuantity() {
        assertThrows(IllegalArgumentException.class, () -> subtotal(125, -1));
    }
}
```

Test one behavioral rule at a time with isolated inputs and useful failure messages. This solution enforces the lesson contracts and has the expected behavior: two passing tests.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

