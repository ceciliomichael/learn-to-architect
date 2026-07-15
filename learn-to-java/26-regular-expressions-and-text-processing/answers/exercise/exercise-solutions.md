# Exercise solution

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

Use regular expressions for bounded text patterns, not as a replacement for parsers and domain validation. This solution enforces the lesson contracts and has the expected behavior: AB and 2048 on separate lines.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

