# Module 25: Date, Time, Locale, and Formatting

## Why this matters

Represent calendar dates, machine instants, time zones, and human formatting as different concerns.

## Contracts to learn

- **Instant:** Instant represents a point on the UTC timeline.
- **LocalDate:** LocalDate is a calendar date without a time or zone.
- **ZonedDateTime:** A zone applies daylight-saving and historical offset rules.
- **Clock:** Passing a Clock makes current-time behavior testable.
- **Locale:** Formatting and parsing for humans require an explicit Locale and pattern policy.

## Complete example

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

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: 15 Jul 2026.

## Deliberate practice

Format the same fixed date for two documented locales and do not compare formatted text as a date.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

Continue to [Module 26](../module-26-regular-expressions-and-text-processing/README.md).

