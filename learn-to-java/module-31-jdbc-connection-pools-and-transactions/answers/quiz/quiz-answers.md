# Quiz answers

1. Applications normally obtain pooled connections from a configured DataSource rather than opening a new physical connection per query.
2. PreparedStatement placeholders bind values, not table names or arbitrary SQL syntax.
3. Connection, Statement, and ResultSet implement AutoCloseable and need deterministic cleanup.
4. Disable auto-commit for a transaction, commit only after all work succeeds, and roll back on failure.
5. Database constraints and Java validation reinforce each other; neither replaces authorization.

