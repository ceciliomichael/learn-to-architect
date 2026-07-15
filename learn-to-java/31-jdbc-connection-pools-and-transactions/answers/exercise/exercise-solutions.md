# Exercise solution

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class Main {
    static void insertProduct(Connection connection, String name, int priceCents)
            throws SQLException {
        if (name == null || name.isBlank() || priceCents < 0) {
            throw new IllegalArgumentException("invalid product");
        }
        String sql = "INSERT INTO products(name, price_cents) VALUES (?, ?)";
        try (PreparedStatement statement = connection.prepareStatement(sql)) {
            statement.setString(1, name.strip());
            statement.setInt(2, priceCents);
            statement.executeUpdate();
        }
    }

    public static void main(String[] args) {
        System.out.println("Supply a reviewed DataSource in the exercise.");
    }
}
```

Treat SQL text, bound values, connections, result sets, and transactions as separate responsibilities. This reference solution preserves all lesson contracts and has this expected behavior: a compileable parameterized JDBC boundary.

Complete the extension in small verified changes. Platform, timing, and external-service results must be recorded as environment-specific evidence rather than universal promises.

