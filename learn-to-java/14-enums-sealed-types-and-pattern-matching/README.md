# Module 14: Enums, Sealed Types, and Pattern Matching

## Why this matters

Represent a closed set of domain states so the compiler can check exhaustive handling.

## Rules to learn

- **enum:** An enum defines named instances from a closed set.
- **sealed type:** A sealed class or interface limits which types may directly implement or extend it.
- **pattern matching:** A type pattern tests a value and introduces a safely typed local name.
- **exhaustive switch:** A switch over a sealed hierarchy can omit default when every permitted type is covered.
- **evolution:** Adding a permitted subtype or enum constant requires reviewing exhaustive consumers.

## Complete example

```java
public class Main {
    sealed interface Result permits Success, Failure {}
    record Success(int value) implements Result {}
    record Failure(String message) implements Result {}

    static String describe(Result result) {
        return switch (result) {
            case Success(int value) -> "value " + value;
            case Failure(String message) -> "error " + message;
        };
    }

    public static void main(String[] args) {
        System.out.println(describe(new Success(42)));
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: value 42.

## Deliberate practice

Add a Failure example and explain why the switch needs no default under Java 21.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

Continue to [Module 15](../15-exceptions-and-resource-cleanup/README.md).

