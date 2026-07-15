# Exercise solution

```java
import java.util.List;
import java.util.function.Predicate;

public class Main {
    static long countMatching(List<Integer> values, Predicate<Integer> keep) {
        long matches = 0;
        for (int value : values) {
            if (keep.test(value)) {
                matches++;
            }
        }
        return matches;
    }

    public static void main(String[] args) {
        int minimum = 70;
        long passing = countMatching(List.of(42, 81, 95, 67),
                score -> score >= minimum);
        System.out.println(passing);
    }
}
```

Pass a small behavior as data while keeping captured state and side effects visible. This solution enforces the lesson contracts and has the expected behavior: 2.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.
