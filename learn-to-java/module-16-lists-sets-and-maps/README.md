# Module 16: Lists, Sets, and Maps

## Why this matters

Choose a collection from the problem rather than from habit.

## Contracts to learn

- **List:** A List preserves encounter order and permits duplicates.
- **Set:** A Set models uniqueness and membership.
- **Map:** A Map associates unique keys with values.
- **mutability:** List.of, Set.of, and Map.of create unmodifiable collections.
- **lookup:** Handle a missing map key explicitly instead of inventing an unsafe sentinel.

## Complete example

```java
import java.util.LinkedHashMap;
import java.util.List;
import java.util.Map;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        List<String> lessons = List.of("values", "loops", "objects");
        Set<String> completed = Set.of("values", "loops");
        Map<String, Integer> minutes = new LinkedHashMap<>();
        minutes.put("values", 20);
        minutes.put("loops", 35);
        for (String lesson : lessons) {
            System.out.println(lesson + " " + completed.contains(lesson)
                    + " " + minutes.getOrDefault(lesson, 0));
        }
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: three ordered lesson status lines.

## Deliberate practice

Add one duplicate input and explain which collection preserves it and which does not.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

Continue to [Module 17](../module-17-generics-and-type-bounds/README.md).

