# Module 01: Playground, JDK Choices, and Tool Versions

## Why this matters

Choose a Java environment deliberately instead of treating every Java installation as identical.

## Rules to learn

- **Playground:** The official Playground is useful for small public examples but not local files or installed libraries.
- **JDK:** A JDK includes the runtime and development tools such as javac, jar, javadoc, and jshell.
- **LTS baseline:** Required course code targets Java 21, independent of the newest feature release.
- **compatibility:** A newer compiler uses --release 21 to check both source features and Java SE APIs.
- **diagnostics:** Read the first compiler diagnostic and source line before editing.

## Complete example

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Java 21 course baseline");
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: Java 21 course baseline.

## Deliberate practice

Run this in the Playground, then compile locally with javac --release 21 -Xlint:all Main.java.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

Continue to [Module 02](../02-source-compilation-class-files-and-main/README.md).

