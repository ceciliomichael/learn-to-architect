# Quiz Answers: Databases, Transactions, and Connection Boundaries

1. Deployed server code imports and runs it, so the package must be available in production rather than only during development.
2. It makes a build fail if code reachable by a Client Component imports the server-only database module.
3. Postgres.js sends those values as query parameters. Their contents cannot become SQL operators or clauses.
4. The callback throws, so the client rolls back the transaction, including the earlier debit.
5. Other code paths or applications may write to the table. The constraint protects the stored invariant at the final boundary.
