# Exercise solution

```java
import java.lang.ref.WeakReference;

public class Main {
    public static void main(String[] args) {
        Object value = new Object();
        WeakReference<Object> observation = new WeakReference<>(value);
        System.out.println(observation.get() != null);
        value = null;
        System.out.println("Collection timing is not a correctness contract.");
    }
}
```

Distinguish automatic memory reclamation from deterministic release of files, sockets, threads, and native resources. This reference solution preserves all lesson contracts and has this expected behavior: true followed by a warning about collection timing.

Complete the extension in small verified changes. Platform, timing, and external-service results must be recorded as environment-specific evidence rather than universal promises.

