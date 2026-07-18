# Module 09: Arrays and Command-Line Arguments

## Why this matters

Use fixed-length sequences and check every external index before reading it.

## Rules to learn

- **length:** An array length is fixed when the array is created.
- **index:** Valid indexes run from zero through length minus one.
- **reference:** Assigning an array variable shares the same array rather than copying elements.
- **copy:** Use Arrays.copyOf when independent storage is required.
- **arguments:** main receives untrusted command-line strings that require count and value checks.

## Complete example

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] scores = {82, 91, 74};
        int[] copy = Arrays.copyOf(scores, scores.length);
        copy[0] = 100;
        String label = args.length == 0 ? "scores" : args[0];
        System.out.println(label + ": " + Arrays.toString(scores));
        System.out.println(Arrays.toString(copy));
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: the original scores followed by an independent copy beginning with 100.

## Deliberate practice

Run with and without a label argument, then deliberately guard access to a second argument.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 10](../10-console-input-parsing-and-validation/README.md).
