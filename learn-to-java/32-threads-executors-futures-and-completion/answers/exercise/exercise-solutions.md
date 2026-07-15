# Exercise solution

```java
import java.time.Duration;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import java.util.concurrent.TimeUnit;

public class Main {
    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        try {
            Future<Integer> left = executor.submit(() -> 20);
            Future<Integer> right = executor.submit(() -> 22);
            int total = left.get(Duration.ofSeconds(1).toMillis(), TimeUnit.MILLISECONDS)
                    + right.get(Duration.ofSeconds(1).toMillis(), TimeUnit.MILLISECONDS);
            System.out.println(total);
        } finally {
            executor.shutdownNow();
        }
    }
}
```

Start concurrent work only when its result, failure, interruption, and shutdown have an owner. This reference solution preserves all lesson contracts and has this expected behavior: 42.

Complete the extension in small verified changes. Platform, timing, and external-service results must be recorded as environment-specific evidence rather than universal promises.

