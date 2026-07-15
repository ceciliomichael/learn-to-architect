# Exercise Solution: Implement and Prove an Atomic Transfer

Use the complete `database.ts` and `transfer.ts` implementations from the lesson.

## Seed data

```sql
INSERT INTO accounts (id, balance_cents)
VALUES ('checking', 5000), ('savings', 1000);
```

## Expected successful result

After `transferMoney({ fromId: "checking", toId: "savings", amountCents: 750 })`:

```text
checking: 4250
savings: 1750
```

## Rollback evidence

Record both balances before each failing call. Catch the expected error, query both rows again, and compare them with the recorded values. A transfer larger than the source balance and a transfer to a missing destination must leave both rows unchanged.

The tagged template parameterizes values to prevent input from changing SQL structure. The transaction makes the two updates one atomic unit. The database constraint rejects a negative stored balance regardless of which application issued the write. None of those protections replaces the others.
