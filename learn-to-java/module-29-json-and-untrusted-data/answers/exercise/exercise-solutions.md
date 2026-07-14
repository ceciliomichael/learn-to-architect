# Exercise solution

```java
import tools.jackson.databind.DeserializationFeature;
import tools.jackson.databind.json.JsonMapper;

public class Main {
    record RawProduct(String name, int priceCents) {}
    record Product(String name, int priceCents) {
        Product {
            if (name == null || name.isBlank() || priceCents < 0) {
                throw new IllegalArgumentException("invalid product");
            }
            name = name.strip();
        }
    }

    public static void main(String[] args) throws Exception {
        JsonMapper mapper = JsonMapper.builder()
                .enable(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES)
                .build();
        RawProduct raw = mapper.readValue(
                "{\"name\":\"Pen\",\"priceCents\":125}", RawProduct.class);
        Product product = new Product(raw.name(), raw.priceCents());
        System.out.println(product);
    }
}
```

Deserialize into a boundary type, enforce size and field rules, then validate before creating trusted domain values. This solution enforces the lesson contracts and has the expected behavior: Product[name=Pen, priceCents=125].

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

