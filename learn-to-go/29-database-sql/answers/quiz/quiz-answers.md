# Quiz Answers: SQL from Go

1. No. It is a concurrency-safe handle to a managed pool.
2. No. Bind values and choose syntax from fixed trusted code.
3. `sql.ErrNoRows`.
4. `rows.Err()` to catch iteration or transport failures.
5. Every early error path then attempts cleanup, while rollback after a successful commit is harmless.
