# Module 39: Documentation, API Compatibility, and Dependency Security

## Why this matters

Treat public behavior and every installed dependency as maintained contracts rather than one-time setup.

## Contracts to learn

- **Javadoc:** Document caller obligations, results, failures, thread rules, units, and examples.
- **compatibility:** Public signatures, exceptions, formats, service behavior, and dependency requirements can all break callers.
- **deprecation:** Deprecation needs a reason, supported replacement, and migration period.
- **dependency review:** Review source, ownership, license, advisories, transitive graph, plugins, and update history.
- **updates:** Update in focused changes, run compatibility tests, inspect resolved diffs, and keep rollback possible.

## Complete example

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

Run or verify with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: 375 and clean javadoc generation.

## Deliberate practice

Run javadoc with doclint and write a dependency review for one library used earlier.

Advanced tools do not replace the earlier rules about validation, cleanup, type safety, and clear ownership.
Continue to [Module 40](../40-build-package-and-release/README.md).

