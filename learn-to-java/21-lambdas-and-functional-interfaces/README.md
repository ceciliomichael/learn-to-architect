# Module 21: Lambdas and Functional Interfaces

## Why this matters

Pass a small behavior as data while keeping captured state and side effects visible.

## Contracts to learn

- **functional interface:** A functional interface has one abstract method.
- **lambda:** A lambda supplies that method's behavior without naming a class.
- **method reference:** A method reference is concise when it remains immediately understandable.
- **capture:** Captured local variables must be final or effectively final.
- **side effects:** Pure transformations are easier to reason about than lambdas that mutate distant state.

## Complete example

```java
import java.util.List;
import java.util.function.Predicate;

public class Main {
    static long countMatching(List<Integer> values, Predicate<Integer> keep) {
        long matches = 0;
        for (int value : values) {
            if (keep.test(value)) {
                matches++;
            }
        }
        return matches;
    }

    public static void main(String[] args) {
        int minimum = 70;
        long passing = countMatching(List.of(42, 81, 95, 67),
                score -> score >= minimum);
        System.out.println(passing);
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: 2.

## Deliberate practice

Pass a different Predicate and then rewrite it as a named method reference where appropriate.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 22](../22-streams-and-optional-values/README.md).
