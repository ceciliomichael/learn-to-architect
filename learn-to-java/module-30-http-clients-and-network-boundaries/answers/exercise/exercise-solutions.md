# Exercise solution

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

Give every outbound request a validated destination, timeout, status policy, body limit, and response validator. This solution enforces the lesson contracts and has the expected behavior: PT5S and https.

The extension should be implemented one rule at a time with the relevant test or compiler check rerun after each change. Dependency versions shown here are explicit inputs and should be reviewed during future updates.

