# Module 33: Virtual Threads and Task Ownership

## Why this matters

Use Java 21 virtual threads for large numbers of blocking tasks without confusing scale with data safety.

## Contracts to learn

- **virtual thread:** A virtual thread is a lightweight Java Thread designed for task-per-request blocking code.
- **not parallelism:** Virtual threads improve the scale of waiting tasks but do not make CPU work faster.
- **ownership:** Keep task handles or use an executor scope so completion and failure remain observable.
- **blocking:** Ordinary blocking I/O is appropriate, while unbounded external work still needs limits and deadlines.
- **shared state:** Virtual threads do not remove races and do not make mutable objects thread-safe.

## Complete example

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

Run or verify with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: 42.

## Deliberate practice

Start several short blocking simulations, keep every Future, and show how one failure is observed.

Advanced tools do not replace the earlier rules about validation, cleanup, type safety, and clear ownership.
Continue to [Module 34](../34-synchronization-and-concurrent-collections/README.md).

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
