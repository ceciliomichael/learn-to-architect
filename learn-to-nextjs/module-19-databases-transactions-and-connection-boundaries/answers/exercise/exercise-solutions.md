# Exercise Solution: Databases, Transactions, and Connection Boundaries

```tsx
await database.transaction(async transaction => {
  await transaction.accounts.debit(fromId, amount);
  await transaction.accounts.credit(toId, amount);
});
```

## Why this works

Keep database access on the server, use a connection strategy supported by the deployment environment, validate records at boundaries, and use transactions for changes that must succeed together. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.