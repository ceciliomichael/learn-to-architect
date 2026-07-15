# Exercise solution

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

Convert raw arguments, environment values, and files into one validated configuration before starting work. This reference solution preserves all lesson contracts and has this expected behavior: the requested name repeated a validated number of times.

Complete the extension in small verified changes. Platform, timing, and external-service results must be recorded as environment-specific evidence rather than universal promises.

