# Module 06: Conditions and Switch Expressions

## Why this matters

Choose program paths from explicit boolean and domain cases.

## Rules to learn

- **if:** An if condition must be boolean; Java does not treat numbers as truth values.
- **order:** The first matching branch runs, so broader conditions must not hide narrower cases.
- **short circuit:** && and || may skip the right operand when the result is already known.
- **switch expression:** A switch expression yields a value and uses arrow cases without accidental fall-through.
- **boundaries:** Test immediately below, at, and above each threshold.

## Complete example

```java
public class Main {
    public static void main(String[] args) {
        int score = 82;
        String level = switch (score / 10) {
            case 10, 9 -> "excellent";
            case 8, 7 -> "good";
            default -> "practice";
        };
        System.out.println(level);
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: good.

## Deliberate practice

Test 69, 70, 89, 90, and 100 and explain the selected case.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

Continue to [Module 07](../module-07-loops-and-repetition/README.md).

