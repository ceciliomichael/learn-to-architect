# Exercise solution

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

Inspect runtime metadata only when a normal typed contract cannot express the boundary. This reference solution preserves all lesson contracts and has this expected behavior: product, name, and priceCents on separate lines.

Complete the extension in small verified changes. Platform, timing, and external-service results must be recorded as environment-specific evidence rather than universal promises.

