# Exercise solution

```java
import java.util.List;

public class Main {
    static double sum(List<? extends Number> values) {
        double total = 0;
        for (Number value : values) {
            total += value.doubleValue();
        }
        return total;
    }

    public static void main(String[] args) {
        System.out.println(sum(List.of(2, 3, 4)));
        System.out.println(sum(List.of(1.5, 2.5)));
    }
}
```

Reuse type-safe behavior without converting everything to Object. This solution enforces the lesson contracts and has the expected behavior: 9.0 and 4.0.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

