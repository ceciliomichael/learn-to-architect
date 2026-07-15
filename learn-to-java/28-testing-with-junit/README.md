# Module 28: Testing with JUnit

## Why this matters

Test one behavioral rule at a time with isolated inputs and useful failure messages.

## Contracts to learn

- **test method:** @Test marks behavior the JUnit engine should execute.
- **assertion:** Assertions compare observable results with the contract.
- **exception test:** assertThrows verifies an expected exception without hiding unrelated failures.
- **isolation:** Tests must not depend on execution order or shared mutable state.
- **test scope:** JUnit belongs in the test dependency scope, not the production runtime.

## Complete example

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

Run or verify this example with mvn test with JUnit Jupiter 6.1.2 in test scope. Expected behavior: two passing tests.

## Deliberate practice

Add zero and overflow boundary tests and give each one a rule-focused name.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

Continue to [Module 29](../29-json-and-untrusted-data/README.md).
