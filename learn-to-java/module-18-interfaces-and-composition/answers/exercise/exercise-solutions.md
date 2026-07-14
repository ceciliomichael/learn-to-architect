# Exercise solution

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

Depend on a small behavior contract and assemble collaborators explicitly. This solution enforces the lesson contracts and has the expected behavior: Report: Progress.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

