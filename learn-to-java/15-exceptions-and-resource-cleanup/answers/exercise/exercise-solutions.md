# Exercise solution

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

Use exceptions for exceptional failures, preserve useful causes, and close resources deterministically. The program demonstrates each rule listed in the lesson and produces first.

For the practice extension, change one behavior at a time and recompile immediately. If your implementation differs, it is still correct when it preserves validation, ownership, and observable behavior.

