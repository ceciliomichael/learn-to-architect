# Module 10: Console Input, Parsing, and Validation

## Why this matters

Separate reading text, converting its shape, and validating its domain meaning.

## Rules to learn

- **line input:** Reading a complete line avoids leftover-newline surprises from mixed token methods.
- **parsing:** Integer.parseInt either returns an int or throws NumberFormatException.
- **domain validation:** A parsed number may still violate allowed ranges.
- **reporting:** A user message should explain how to correct input without exposing internals.
- **resource ownership:** Close a Scanner only when the program is finished with the underlying input stream.

## Complete example

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        try (Scanner scanner = new Scanner(System.in)) {
            System.out.print("Quantity: ");
            String text = scanner.nextLine().trim();
            try {
                int quantity = Integer.parseInt(text);
                if (quantity < 1 || quantity > 100) {
                    System.out.println("Use a quantity from 1 through 100.");
                    return;
                }
                System.out.println("Accepted: " + quantity);
            } catch (NumberFormatException error) {
                System.out.println("Enter a whole number.");
            }
        }
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: a prompt and either accepted input or a correction message.

## Deliberate practice

Test blank text, letters, 0, 1, 100, and 101.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 11](../11-classes-and-objects/README.md).
