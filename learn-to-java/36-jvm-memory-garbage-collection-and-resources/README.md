# Module 36: JVM Memory, Garbage Collection, and Resources

## Why this matters

Distinguish automatic memory reclamation from deterministic release of files, sockets, threads, and native resources.

## Contracts to learn

- **reachability:** The collector may reclaim an object only after it is no longer strongly reachable.
- **timing:** System.gc is only a request and cleanup logic must not depend on collection timing.
- **resource:** Garbage collection does not replace close for operating-system and native resources.
- **retention:** A static collection, cache, listener, or ThreadLocal can retain objects unintentionally.
- **measurement:** Use heap evidence and allocation profiles rather than guessing from source alone.

## Complete example

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

Run or verify with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: true followed by a warning about collection timing.

## Deliberate practice

Find three resources that require close even though their wrapper objects are garbage collected.

Advanced tools do not replace the earlier rules about validation, cleanup, type safety, and clear ownership.
Continue to [Module 37](../37-measurement-jfr-and-jmh/README.md).

