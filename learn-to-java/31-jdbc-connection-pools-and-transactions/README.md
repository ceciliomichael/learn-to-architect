# Module 31: JDBC, Connection Pools, and Transactions

## Why this matters

Treat SQL text, bound values, connections, result sets, and transactions as separate responsibilities.

## Contracts to learn

- **DataSource:** Applications normally obtain pooled connections from a configured DataSource rather than opening a new physical connection per query.
- **binding:** PreparedStatement placeholders bind values, not table names or arbitrary SQL syntax.
- **cleanup:** Connection, Statement, and ResultSet implement AutoCloseable and need deterministic cleanup.
- **transaction:** Disable auto-commit for a transaction, commit only after all work succeeds, and roll back on failure.
- **boundary:** Database constraints and Java validation reinforce each other; neither replaces authorization.

## Complete example

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

Run or verify with javac --release 21 -Xlint:all Main.java, then java Main. Expected behavior: a compileable parameterized JDBC boundary.

## Deliberate practice

Use a disposable test database and prove commit, rollback, unique constraints, and cleanup behavior.

Advanced tools do not replace the earlier rules about validation, cleanup, type safety, and clear ownership.
Continue to [Module 32](../32-threads-executors-futures-and-completion/README.md).

