# Module 24: Files, Paths, and Buffered I/O

## Why this matters

Treat paths and file contents as external input with explicit encoding, size, and cleanup rules.

## Contracts to learn

- **Path:** Path represents a filesystem path without assuming one operating-system separator.
- **encoding:** Specify UTF-8 or another documented charset instead of relying on a platform default.
- **buffering:** Buffered readers and writers reduce repeated small I/O operations.
- **bounded input:** Do not read an untrusted file into unlimited memory.
- **cleanup:** Use try-with-resources for opened streams and readers.

## Complete example

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Main {
    public static void main(String[] args) throws IOException {
        Path file = Files.createTempFile("java-course-", ".txt");
        try {
            Files.writeString(file, "one\ntwo\n", StandardCharsets.UTF_8);
            try (BufferedReader reader = Files.newBufferedReader(file, StandardCharsets.UTF_8)) {
                System.out.println(reader.readLine());
            }
        } finally {
            Files.deleteIfExists(file);
        }
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: one.

## Deliberate practice

Count lines by streaming them and preserve deletion even if reading fails.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 25](../25-date-time-locale-and-formatting/README.md).
