# Module 26: Regular Expressions and Text Processing

## Why this matters

Use regular expressions for bounded text patterns, not as a replacement for parsers and domain validation.

## Contracts to learn

- **Pattern:** Compile a reused regular expression once as a Pattern.
- **Matcher:** Matcher holds state for one input and should not be shared carelessly.
- **matches:** matches requires the entire input; find searches for a matching region.
- **quoting:** Pattern.quote treats external text literally instead of as regex syntax.
- **complexity:** Avoid vulnerable nested repetition and set input limits for untrusted text.

## Complete example

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Main {
    private static final Pattern CODE =
            Pattern.compile("(?<prefix>[A-Z]{2})-(?<number>[0-9]{4})");

    public static void main(String[] args) {
        Matcher matcher = CODE.matcher("AB-2048");
        if (matcher.matches()) {
            System.out.println(matcher.group("prefix"));
            System.out.println(matcher.group("number"));
        }
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: AB and 2048 on separate lines.

## Deliberate practice

Test valid and invalid boundaries, then explain why a second domain check may still be necessary.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 27](../27-maven-gradle-and-installed-dependencies/README.md).
