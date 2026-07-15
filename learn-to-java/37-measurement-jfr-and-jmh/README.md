# Module 37: Measurement, JFR, and JMH

## Why this matters

Optimize only after a representative release-like workload and profiler identify a user-relevant bottleneck.

## Contracts to learn

- **warmup:** JIT compilation and class loading make early measurements unrepresentative.
- **JMH:** JMH handles warmup, forks, result consumption, and statistical sampling for microbenchmarks.
- **JFR:** Java Flight Recorder captures runtime events for broader application diagnosis.
- **goal:** Latency, throughput, memory, startup, and code size are different performance goals.
- **verification:** After optimization, confirm equivalent results and measure again.

## Complete example

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

Run or verify with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: the correct sum and a machine-specific duration.

## Deliberate practice

Explain why this timer is educational but not a replacement for a JMH benchmark with forks.

Advanced tools do not replace the earlier rules about validation, cleanup, type safety, and clear ownership.
Continue to [Module 38](../38-command-line-configuration-and-logging/README.md).

