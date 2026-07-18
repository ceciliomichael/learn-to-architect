# Module 05: Operators, Conversions, Overflow, and Math

## Why this matters

Calculate deliberately while recognizing integer division, narrowing, and overflow.

## Rules to learn

- **precedence:** Parentheses communicate intended grouping even when default precedence is known.
- **integer division:** Dividing two integers discards any fractional part.
- **promotion:** Arithmetic may promote smaller numeric operands before calculation.
- **narrowing:** A narrowing cast can lose range or precision and needs an explicit decision.
- **overflow:** Use Math exact methods when overflow must become an error rather than wrap.

## Complete example

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

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: 375 125.00.

## Deliberate practice

Remove the double cast to observe integer division, then test Math.addExact with an overflowing calculation.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 06](../06-conditions-and-switch-expressions/README.md).
