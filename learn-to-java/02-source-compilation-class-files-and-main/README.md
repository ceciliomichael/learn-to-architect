# Module 02: Source Files, Compilation, Class Files, and Main

## Why this matters

Trace a program from readable source through bytecode to JVM execution.

## Rules to learn

- **file naming:** A public class named Main belongs in Main.java.
- **compilation:** javac checks source and writes class files containing JVM bytecode.
- **entry point:** The JVM starts public static void main(String[] args).
- **launcher:** Run java Main without adding .java or .class after separate compilation.
- **output directory:** Use javac -d to keep generated class files away from source files in larger projects.

## Complete example

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("source");
        System.out.println("compile");
        System.out.println("run");
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: three lines: source, compile, run.

## Deliberate practice

Compile into an out directory with javac --release 21 -d out Main.java and run with java -cp out Main.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

Continue to [Module 03](../03-variables-primitive-types-and-constants/README.md).

