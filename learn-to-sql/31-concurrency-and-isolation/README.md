# Module 31: Concurrency, Locking, and Isolation

## What you will learn

You will understand overlapping transactions, common read anomalies, SQLite writer limits, PostgreSQL isolation, and safe retries.

## Concurrency creates timing questions

Two transactions can overlap. Isolation defines which changes each transaction can observe and what conflicts the database prevents.

Common anomaly names are:

- Dirty read: reading another transaction's uncommitted value
- Nonrepeatable read: rereading one row and seeing a newly committed change
- Phantom read: repeating a condition and seeing a changed set of rows
- Serialization anomaly: the combined result could not match any serial order of the transactions

These names describe behavior. Do not assume an isolation level from its label alone; read the target product's guarantees.

## SQLite serializes writers

Separate SQLite connections are isolated. Except for a discouraged shared-cache plus `read_uncommitted` combination, one connection does not see another connection's uncommitted changes.

SQLite allows many readers but only one writer at a time. In rollback-journal mode, a writer can temporarily block readers during commit. Write-ahead logging mode lets readers and a writer overlap more, while still allowing only one writer.

```sql
PRAGMA journal_mode = WAL;
PRAGMA busy_timeout = 5000;
```

These are deployment decisions, not universal performance switches. A busy timeout waits for a lock for a limited time. Applications must still handle `SQLITE_BUSY` and retry appropriate transactions.

`BEGIN IMMEDIATE` acquires the write transaction early, so failure happens before later business work:

```sql
BEGIN IMMEDIATE;
```

## PostgreSQL Read Committed

PostgreSQL defaults to Read Committed. Each command sees a snapshot from the start of that command. Two selects in one transaction can therefore see different committed data.

```sql
BEGIN ISOLATION LEVEL READ COMMITTED;
```

PostgreSQL Repeatable Read keeps a stable transaction snapshot and also prevents phantom reads, which is stronger than the minimum SQL standard requirement for that level. Conflicting writes can still cause a serialization-style failure that must be retried.

## PostgreSQL Serializable

```sql
BEGIN ISOLATION LEVEL SERIALIZABLE;
```

Serializable aims for results equivalent to transactions running one at a time. PostgreSQL may abort one transaction with a serialization failure to preserve that guarantee. The application must retry the entire transaction from the beginning with fresh reads.

## Row locking is targeted coordination

PostgreSQL provides row locks such as:

```sql
SELECT account_id, balance_cents
FROM accounts
WHERE account_id = 1
FOR UPDATE;
```

This can coordinate a following update, but locks can wait and deadlock. Acquire locks in a consistent order, keep transactions short, and handle deadlock errors by retrying the whole unit.

SQLite does not support `SELECT FOR UPDATE`. Its locking model is database-file oriented.

## Retry safely

A safe retry loop belongs in application code:

1. Begin a new transaction.
2. Repeat all reads and decisions.
3. Apply changes.
4. Commit.
5. On a documented transient busy, deadlock, or serialization error, roll back, wait with bounded random delay, and retry a limited number of times.

Operations should be idempotent or use a request key so a lost response does not create duplicate business actions.

## Common mistakes

### Retrying only the failed statement

Earlier reads may no longer be valid. Retry the whole transaction.

### Keeping a transaction open during user input

It holds resources and widens the conflict window.

### Assuming SQLite scales through more writers

It supports one writer. Short writes and correct workload choice matter.

## Check your understanding

You are ready when you can explain one-writer SQLite behavior and why PostgreSQL serializable failures are expected safety signals.
