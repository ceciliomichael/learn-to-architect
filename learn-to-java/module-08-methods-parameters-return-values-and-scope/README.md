# Module 08: Methods, Parameters, Return Values, and Scope

## Why this matters

Give one focused behavior a name, explicit inputs, and a checked output contract.

## Rules to learn

- **parameters:** Parameters are local names initialized from caller arguments.
- **return:** A non-void method returns a compatible value on every reachable path.
- **scope:** A local name exists only inside its declaring block.
- **overloading:** Overloaded methods differ by parameter lists; return type alone cannot distinguish them.
- **varargs:** A varargs parameter is received as an array and must be last.

## Complete example

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

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: 375.

## Deliberate practice

Add a tax method with its own validation and keep main limited to orchestration.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

Continue to [Module 09](../module-09-arrays-and-command-line-arguments/README.md).

