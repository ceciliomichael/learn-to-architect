# Exercise solution

```java
public class Main {
    static long sum(int limit) {
        long total = 0;
        for (int value = 0; value < limit; value++) {
            total += value;
        }
        return total;
    }

    public static void main(String[] args) {
        for (int warmup = 0; warmup < 10_000; warmup++) {
            sum(1_000);
        }
        long start = System.nanoTime();
        long result = sum(1_000_000);
        long elapsed = System.nanoTime() - start;
        System.out.println(result);
        System.out.println("elapsed ns: " + elapsed);
    }
}
```

Optimize only after a representative release-like workload and profiler identify a user-relevant bottleneck. This reference solution preserves all lesson contracts and has this expected behavior: the correct sum and a machine-specific duration.

Complete the extension in small verified changes. Platform, timing, and external-service results must be recorded as environment-specific evidence rather than universal promises.

