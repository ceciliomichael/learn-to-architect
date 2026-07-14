# Exercise solution

```java
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.atomic.LongAdder;
import java.util.stream.IntStream;

public class Main {
    public static void main(String[] args) {
        ConcurrentHashMap<String, LongAdder> counts = new ConcurrentHashMap<>();
        IntStream.range(0, 1_000).parallel().forEach(number ->
                counts.computeIfAbsent("events", key -> new LongAdder()).increment());
        System.out.println(counts.get("events").sum());
    }
}
```

Protect shared invariants with the smallest synchronization boundary that makes compound actions atomic. This reference solution preserves all lesson contracts and has this expected behavior: 1000.

Complete the extension in small verified changes. Platform, timing, and external-service results must be recorded as environment-specific evidence rather than universal promises.

