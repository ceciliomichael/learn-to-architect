# Module 34: Synchronization and Concurrent Collections

## Why this matters

Protect shared invariants with the smallest synchronization boundary that makes compound actions atomic.

## Contracts to learn

- **race:** A data race can lose updates or expose stale state even when individual reads look harmless.
- **synchronized:** synchronized provides mutual exclusion and a happens-before relationship around the same monitor.
- **lock scope:** Keep critical sections short and never hold a lock across slow external I/O.
- **concurrent collection:** ConcurrentHashMap supports concurrent access but multi-step domain rules may still need atomic map methods.
- **atomic value:** Atomic classes suit focused counters and flags, not arbitrary multi-field invariants.

## Complete example

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

Run or verify with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: 1000.

## Deliberate practice

Replace the atomic update with a broken get-then-put sequence and explain the race before restoring it.

Advanced tools do not replace the earlier rules about validation, cleanup, type safety, and clear ownership.
Continue to [Module 35](../35-reflection-annotations-and-runtime-types/README.md).

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
