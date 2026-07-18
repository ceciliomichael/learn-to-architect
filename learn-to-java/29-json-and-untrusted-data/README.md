# Module 29: JSON and Untrusted Data

## Why this matters

Deserialize into a boundary type, enforce size and field rules, then validate before creating trusted domain values.

## Contracts to learn

- **dependency:** Jackson 3 uses tools.jackson package names and must be installed through the reviewed build.
- **shape:** Deserialization checks representable shape, not business validity or authorization.
- **unknown fields:** Choose deliberately whether unknown fields are rejected for a strict contract.
- **size:** Limit bytes and nesting before parsing untrusted JSON.
- **domain conversion:** Convert a raw input record into a validated domain type before behavior uses it.

## Complete example

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

Run or verify this example with mvn test or mvn exec:java with tools.jackson.core:jackson-databind:3.1.3. Expected behavior: Product[name=Pen, priceCents=125].

## Deliberate practice

Reject blank names, negative prices, extra fields, oversized input, and trailing JSON values.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 30](../30-http-clients-and-network-boundaries/README.md).
