# Module 32: Threads, Executors, Futures, and Completion

## Why this matters

Start concurrent work only when its result, failure, interruption, and shutdown have an owner.

## Contracts to learn

- **task:** A task should have explicit input and return a result or failure.
- **executor:** An ExecutorService owns worker resources and requires shutdown.
- **Future:** Future.get observes completion and can report execution, interruption, or timeout failures.
- **interruption:** Restore or propagate interruption instead of silently consuming it.
- **timeout:** A caller deadline prevents indefinite waiting but does not automatically make task side effects reversible.

## Complete example

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

Run or verify with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: 42.

## Deliberate practice

Make one task fail and report its cause without losing executor shutdown.

Advanced tools do not replace the earlier rules about validation, cleanup, type safety, and clear ownership.
Continue to [Module 33](../33-virtual-threads-and-task-ownership/README.md).

