# Module 04: Strings, Characters, Unicode, and Text Blocks

## Why this matters

Handle text without assuming one char always equals one visible symbol.

## Rules to learn

- **String:** Strings are immutable, so operations return new values rather than changing existing text.
- **comparison:** Use equals for text content because == compares object references.
- **char:** A char is one UTF-16 code unit and may be only part of a Unicode code point.
- **code points:** Use codePoints when complete Unicode code points matter.
- **text blocks:** Text blocks make intentional multi-line source text readable.

## Complete example

```java
public class Main {
    public static void main(String[] args) {
        String name = "Java";
        String separate = new String("Java");
        String note = """
                Learn carefully.
                Practice daily.
                """;
        System.out.println(name.equals(separate));
        System.out.println(name.codePointCount(0, name.length()));
        System.out.print(note);
    }
}
```

Compile with `javac --release 21 -Xlint:all Main.java` and run with `java Main`. Expected behavior: true, 4, and two note lines.

## Deliberate practice

Add a supplementary Unicode symbol and compare String length with codePointCount.

Type the code instead of pasting it. Predict the result first, then use compiler feedback to check your reasoning.

Continue to [Module 05](../module-05-operators-conversions-overflow-and-math/README.md).

