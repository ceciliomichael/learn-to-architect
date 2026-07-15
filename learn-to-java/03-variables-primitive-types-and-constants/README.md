# Module 03: Variables, Primitive Types, and Constants

## Why this matters

Store values with types that match their meaning and make reassignment rules visible.

## Rules to learn

- **primitive types:** Java has boolean, character, integer, and floating-point primitive types.
- **declaration:** A local variable needs a type, name, and value before it is read.
- **final:** A final variable cannot be assigned again after initialization.
- **var:** var infers a local type from an initializer and does not make Java dynamically typed.
- **range:** Choose a numeric type whose range covers valid domain values.

## Complete example

```java
public class Main {
    public static void main(String[] args) {
        int lessons = 3;
        long visitors = 2_000_000L;
        double price = 19.95;
        boolean open = true;
        char grade = 'A';
        final int maxLessons = 40;
        System.out.printf("%d %d %.2f %b %c %d%n",
                lessons, visitors, price, open, grade, maxLessons);
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: 3 2000000 19.95 true A 40.

## Deliberate practice

Change every value, then make one incompatible assignment and study the compiler message before restoring valid code.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

Continue to [Module 04](../04-strings-characters-unicode-and-text-blocks/README.md).

