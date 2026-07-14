# Module 35: Reflection, Annotations, and Runtime Types

## Why this matters

Inspect runtime metadata only when a normal typed contract cannot express the boundary.

## Contracts to learn

- **Class:** Class objects describe runtime types after generic erasure.
- **annotation:** An annotation records metadata; behavior changes only when a tool or program reads it.
- **encapsulation:** Do not break private access merely because reflection can request it.
- **validation:** Reflective names and values from outside the program remain untrusted input.
- **cost:** Reflection adds runtime failure modes and should be isolated behind a typed API.

## Complete example

```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.reflect.RecordComponent;

public class Main {
    @Retention(RetentionPolicy.RUNTIME)
    @interface Label { String value(); }

    @Label("product")
    record Product(String name, int priceCents) {}

    public static void main(String[] args) {
        Label label = Product.class.getAnnotation(Label.class);
        System.out.println(label.value());
        for (RecordComponent component : Product.class.getRecordComponents()) {
            System.out.println(component.getName());
        }
    }
}
```

Run or verify with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: product, name, and priceCents on separate lines.

## Deliberate practice

Reject a class that lacks the annotation instead of assuming getAnnotation is non-null.

Advanced tools do not replace the earlier rules about validation, cleanup, type safety, and clear ownership.
Continue to [Module 36](../module-36-jvm-memory-garbage-collection-and-resources/README.md).

