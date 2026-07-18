# Module 30: HTTP Clients and Network Boundaries

## Why this matters

Give every outbound request a validated destination, timeout, status policy, body limit, and response validator.

## Contracts to learn

- **client reuse:** Reuse one HttpClient so configuration and connections are shared.
- **URI policy:** Parse the URI and restrict schemes, hosts, and redirects when input controls the destination.
- **timeout:** Set connect and request timeouts based on an application deadline.
- **status:** Treat non-success status codes according to the remote API contract.
- **body limit:** Limit response bytes before decoding and validate all decoded values.

## Complete example

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.time.Duration;

public class Main {
    public static void main(String[] args) {
        HttpClient client = HttpClient.newBuilder()
                .connectTimeout(Duration.ofSeconds(5))
                .followRedirects(HttpClient.Redirect.NEVER)
                .build();
        HttpRequest request = HttpRequest.newBuilder(URI.create("https://example.com/"))
                .timeout(Duration.ofSeconds(10))
                .GET()
                .build();
        System.out.println(client.connectTimeout().orElseThrow());
        System.out.println(request.uri().getScheme());
    }
}
```

Run or verify this example with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: PT5S and https.

## Deliberate practice

Write a destination validator before sending any request, then describe how you would bound the response body.

Keep build files and resolved dependency changes under review. Do not weaken a validator or suppress a diagnostic merely to make an example pass.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).

Continue to [Module 31](../31-jdbc-connection-pools-and-transactions/README.md).
