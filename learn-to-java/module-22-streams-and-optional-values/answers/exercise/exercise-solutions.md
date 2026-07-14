# Exercise solution

```java
import java.util.List;
import java.util.Optional;

public class Main {
    static Optional<String> firstPassing(List<Integer> scores) {
        return scores.stream()
                .filter(score -> score >= 70)
                .map(score -> "score " + score)
                .findFirst();
    }

    public static void main(String[] args) {
        System.out.println(firstPassing(List.of(42, 81, 95)).orElse("none"));
    }
}
```

Describe a collection pipeline while treating absence as an explicit possibility. This solution enforces the lesson contracts and has the expected behavior: score 81.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

