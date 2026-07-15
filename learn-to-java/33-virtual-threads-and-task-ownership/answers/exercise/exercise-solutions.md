# Exercise solution

```java
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class Main {
    public static void main(String[] args) throws Exception {
        try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
            Future<Integer> left = executor.submit(() -> 20);
            Future<Integer> right = executor.submit(() -> 22);
            System.out.println(left.get() + right.get());
        }
    }
}
```

Use Java 21 virtual threads for large numbers of blocking tasks without confusing scale with data safety. This reference solution preserves all lesson contracts and has this expected behavior: 42.

Complete the extension in small verified changes. Platform, timing, and external-service results must be recorded as environment-specific evidence rather than universal promises.

