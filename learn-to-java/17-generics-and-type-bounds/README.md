# Module 17: Generics and Type Bounds

## Why this matters

Reuse type-safe behavior without converting everything to Object.

## Contracts to learn

- **type parameter:** A type parameter stands for a caller-selected reference type.
- **invariance:** List<Integer> is not a subtype of List<Number>.
- **upper bound:** ? extends T is useful for reading values as T.
- **lower bound:** ? super T is useful for safely adding T values.
- **erasure:** Most generic type arguments are erased at runtime, so some type tests and arrays are restricted.

## Complete example

```java
import java.util.List;

public class Main {
    static double sum(List<? extends Number> values) {
        double total = 0;
        for (Number value : values) {
            total += value.doubleValue();
        }
        return total;
    }

    public static void main(String[] args) {
        System.out.println(sum(List.of(2, 3, 4)));
        System.out.println(sum(List.of(1.5, 2.5)));
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: 9.0 and 4.0.

## Deliberate practice

Write a copy method using a source with extends and a destination with super.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 18](../18-interfaces-and-composition/README.md).
