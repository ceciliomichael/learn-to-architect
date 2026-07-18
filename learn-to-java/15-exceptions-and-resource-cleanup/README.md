# Module 15: Exceptions and Resource Cleanup

## Why this matters

Use exceptions for exceptional failures, preserve useful causes, and close resources deterministically.

## Rules to learn

- **checked exception:** A checked exception must be handled or declared, making the failure part of the method contract.
- **runtime exception:** Runtime exceptions commonly report violated programming or input contracts.
- **catch specificity:** Catch only failures the current boundary can handle meaningfully.
- **cause:** Wrap with a cause when adding context so diagnostics keep the original failure.
- **try with resources:** Try-with-resources closes AutoCloseable values in reverse acquisition order.

## Complete example

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.StringReader;

public class Main {
    static String firstLine(String text) throws IOException {
        try (BufferedReader reader = new BufferedReader(new StringReader(text))) {
            String line = reader.readLine();
            if (line == null) {
                throw new IOException("input has no line");
            }
            return line;
        }
    }

    public static void main(String[] args) {
        try {
            System.out.println(firstLine("first\nsecond"));
        } catch (IOException error) {
            System.err.println("read failed: " + error.getMessage());
        }
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: first.

## Deliberate practice

Change the method to read two lines and keep cleanup automatic even when validation fails.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 16](../16-lists-sets-and-maps/README.md).
