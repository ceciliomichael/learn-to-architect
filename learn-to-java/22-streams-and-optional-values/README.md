# Module 22: Streams and Optional Values

## Why this matters

Describe a collection pipeline while treating absence as an explicit possibility.

## Contracts to learn

- **stream:** A stream pipeline is lazy until a terminal operation requests values.
- **intermediate operation:** map and filter describe transformations without changing the source collection.
- **terminal operation:** collect, count, reduce, and forEach consume a stream pipeline.
- **Optional:** Optional represents a result that may be absent and is mainly useful as a return type.
- **readability:** Use a loop when a pipeline hides branching, checked failures, or important state.

## Complete example

```java
import java.util.List;
import java.util.Optional;

public class Main {
    static Optional<String> firstPassing(List<Integer> scores) {
        return scores.stream()
                .filter(score -> score >= 70)
                .map(score -> "score " + score)
                .findFirst();
    }

    public static void main(String[] args) {
        System.out.println(firstPassing(List.of(42, 81, 95)).orElse("none"));
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: score 81.

## Deliberate practice

Return none for an empty input and handle it without get or orElseThrow.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 23](../23-packages-access-classpaths-modules-and-jars/README.md).
