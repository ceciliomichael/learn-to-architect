# Exercise solution

```java
import java.time.Clock;
import java.time.Instant;
import java.time.LocalDate;
import java.time.ZoneOffset;
import java.time.format.DateTimeFormatter;
import java.util.Locale;

public class Main {
    public static void main(String[] args) {
        Clock clock = Clock.fixed(Instant.parse("2026-07-15T00:00:00Z"), ZoneOffset.UTC);
        LocalDate date = LocalDate.now(clock);
        DateTimeFormatter format = DateTimeFormatter.ofPattern("dd MMM uuuu", Locale.US);
        System.out.println(date.format(format));
    }
}
```

Represent calendar dates, machine instants, time zones, and human formatting as different concerns. This solution enforces the lesson contracts and has the expected behavior: 15 Jul 2026.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

