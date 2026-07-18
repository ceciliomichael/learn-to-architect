# Module 38: Command-Line Configuration and Logging

## Why this matters

Convert raw arguments, environment values, and files into one validated configuration before starting work.

## Contracts to learn

- **precedence:** Document whether command line, environment, file, or default wins for each setting.
- **typed config:** Domain code should receive validated typed configuration rather than raw strings.
- **exit status:** Use zero for success and a documented nonzero status for failure.
- **streams:** Normal output belongs on stdout and diagnostics belong on stderr.
- **logging:** Use stable fields and levels while excluding secrets and sensitive payloads.

## Complete example

```java
public class Main {
    record Config(String name, int count) {
        Config {
            if (name == null || name.isBlank() || count < 1 || count > 10) {
                throw new IllegalArgumentException("usage: java Main NAME COUNT");
            }
            name = name.strip();
        }
    }

    public static void main(String[] args) {
        try {
            if (args.length != 2) throw new IllegalArgumentException();
            Config config = new Config(args[0], Integer.parseInt(args[1]));
            for (int index = 0; index < config.count(); index++) {
                System.out.println(config.name());
            }
        } catch (RuntimeException error) {
            System.err.println("usage: java Main NAME COUNT, with COUNT from 1 through 10");
            System.exit(2);
        }
    }
}
```

Run or verify with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: the requested name repeated a validated number of times.

## Deliberate practice

Test missing, extra, blank, nonnumeric, zero, ten, and eleven arguments.

Advanced tools do not replace the earlier rules about validation, cleanup, type safety, and clear ownership.
Continue to [Module 39](../39-documentation-api-compatibility-and-dependency-security/README.md).

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
