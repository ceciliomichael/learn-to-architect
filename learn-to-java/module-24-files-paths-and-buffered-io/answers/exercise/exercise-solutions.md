# Exercise solution

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

Treat paths and file contents as external input with explicit encoding, size, and cleanup rules. This solution enforces the lesson contracts and has the expected behavior: one.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

