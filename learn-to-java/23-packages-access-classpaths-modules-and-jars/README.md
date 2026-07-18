# Module 23: Packages, Access, Classpaths, Modules, and JARs

## Why this matters

Organize source and compiled code so names, visibility, and runtime lookup agree.

## Contracts to learn

- **package:** A package name corresponds to source and class directory structure.
- **access:** public, protected, package-private, and private expose different boundaries.
- **classpath:** The classpath tells tools where to find unnamed-module classes and JARs.
- **module:** module-info.java declares named-module requirements and exported packages.
- **JAR:** A JAR packages classes and resources; it does not automatically include dependency JARs.

## Complete example

```java
public class Main {
    public static void main(String[] args) {
        Module module = Main.class.getModule();
        Package location = Main.class.getPackage();
        System.out.println("named module: " + module.isNamed());
        System.out.println("package: " + location.getName());
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: named module: false and an empty package name.

## Deliberate practice

Move Main into package course.app, compile with -d out, and create a runnable JAR with an explicit main class.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 24](../24-files-paths-and-buffered-io/README.md).
