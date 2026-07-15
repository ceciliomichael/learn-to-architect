# Module 18: Interfaces and Composition

## Why this matters

Depend on a small behavior contract and assemble collaborators explicitly.

## Contracts to learn

- **interface:** An interface names behavior without deciding one storage design.
- **implementation:** A class implements every required abstract method.
- **composition:** Composition models a has-a or uses-a relationship.
- **dependency injection:** Passing a collaborator makes dependencies visible and replaceable in tests.
- **default method:** A default interface method should provide behavior valid for all implementations.

## Complete example

```java
public class Main {
    interface Sender {
        void send(String message);
    }

    static final class ConsoleSender implements Sender {
        public void send(String message) {
            System.out.println(message);
        }
    }

    static final class ReportService {
        private final Sender sender;
        ReportService(Sender sender) { this.sender = sender; }
        void publish(String title) { sender.send("Report: " + title); }
    }

    public static void main(String[] args) {
        new ReportService(new ConsoleSender()).publish("Progress");
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: Report: Progress.

## Deliberate practice

Add a RecordingSender that stores the last message without changing ReportService.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

Continue to [Module 19](../19-inheritance-and-polymorphism/README.md).

