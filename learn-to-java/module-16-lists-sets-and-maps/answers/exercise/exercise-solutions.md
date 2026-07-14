# Exercise solution

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

Choose a collection from the problem rather than from habit. This solution enforces the lesson contracts and has the expected behavior: three ordered lesson status lines.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

