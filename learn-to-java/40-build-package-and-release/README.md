# Module 40: Build, Package, and Release Java Programs

## Why this matters

Produce a tested artifact with a known source, toolchain, dependency graph, target runtime, integrity value, and rollback plan.

## Contracts to learn

- **clean build:** Release from a clean checkout with locked or reviewed dependency resolution.
- **artifact:** Inspect the JAR contents and launch it in an environment like production.
- **runtime:** jlink can create a custom runtime and jpackage can create native installers, each with platform requirements.
- **provenance:** Record source commit, JDK, build command, dependencies, target, checksums, and signing process.
- **rollback:** Keep a previous known-good artifact and write rollback verification before rollout.

## Complete example

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("release candidate");
    }
}
```

Run or verify with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: a Java 21-compatible class that can be packaged into a runnable JAR.

## Deliberate practice

Create a runnable JAR locally, inspect it with jar --list, calculate SHA-256, test startup and failure behavior, and do not publish it.

Advanced tools do not replace the earlier rules about validation, cleanup, type safety, and clear ownership.
This completes the planned Java path. There is intentionally no miscellaneous module or final assessment.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
