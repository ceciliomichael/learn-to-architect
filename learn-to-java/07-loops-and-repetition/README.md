# Module 07: Loops and Repetition

## Why this matters

Repeat work with a visible starting state, continuation rule, and progress step.

## Rules to learn

- **for:** Use for when initialization, condition, and update form one clear unit.
- **while:** Use while when repetition depends on a condition with no natural counter.
- **enhanced for:** Use enhanced for to read each array or collection value without an index.
- **termination:** A loop must progress toward stopping unless its long-running policy is explicit.
- **break and continue:** Use break and continue only when they make control flow clearer than another condition.

## Complete example

```java
public class Main {
    public static void main(String[] args) {
        int total = 0;
        for (int number = 1; number <= 5; number++) {
            total += number;
        }
        System.out.println(total);
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: 15.

## Deliberate practice

Rewrite the calculation with while and with an enhanced for loop over an array.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

Continue to [Module 08](../08-methods-parameters-return-values-and-scope/README.md).

