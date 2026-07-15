# Module 19: Databases, Transactions, and Connection Boundaries

## Before you start

This module assumes you completed the SQL course and the earlier Next.js modules on server code, validation, authentication, and authorization. Use only a disposable PostgreSQL database.

## What you will learn

By the end of this module, you will be able to:

- install and configure one concrete PostgreSQL client
- keep database credentials and queries in server-only modules
- use parameterized SQL instead of joining user input into query text
- perform related writes in one transaction
- explain how connection limits depend on the deployment environment

## 1. Install the database client

Inside `nextjs-course`, run:

```text
npm install postgres
```

The package is needed by deployed server code, so it is a production dependency. This module uses Postgres.js directly so the transaction and SQL remain visible. An ORM can be introduced later, but it does not remove the need to understand transactions or constraints.

Create `.env.local` with a disposable connection URL:

```text
DATABASE_URL=postgres://course_user:course_password@localhost:5432/nextjs_course
```

Do not commit this file. Add a redacted `.env.example` that contains the variable name without a real password.

## 2. Create a server-only connection module

Create `app/lib/database.ts`:

```ts
import "server-only";
import postgres from "postgres";

const databaseUrl = process.env.DATABASE_URL;

if (databaseUrl === undefined || databaseUrl.length === 0) {
  throw new Error("DATABASE_URL is required");
}

export const sql = postgres(databaseUrl, {
  max: 5,
  idle_timeout: 20,
  connect_timeout: 10,
});
```

`server-only` makes an accidental import into a Client Component fail during the build. The small connection limit is a course default, not a universal production value. A long-running server, a serverless platform, and a database proxy have different connection behavior. Read the deployment provider's database guidance before choosing a production limit.

## 3. Create constraints in the database

Run this migration through the SQL workflow established in the SQL course:

```sql
CREATE TABLE accounts (
  id text PRIMARY KEY,
  balance_cents integer NOT NULL CHECK (balance_cents >= 0)
);
```

The check constraint protects the rule even if another program writes to the table. Application validation improves errors, but database constraints remain the final storage boundary.

## 4. Transfer money atomically

Create `app/lib/transfer.ts`:

```ts
import "server-only";
import { sql } from "./database";

export type TransferInput = {
  fromId: string;
  toId: string;
  amountCents: number;
};

export async function transferMoney(input: TransferInput): Promise<void> {
  if (input.fromId === input.toId) {
    throw new Error("Accounts must be different");
  }

  if (!Number.isSafeInteger(input.amountCents) || input.amountCents <= 0) {
    throw new Error("Amount must be a positive integer number of cents");
  }

  await sql.begin(async transaction => {
    const debited = await transaction<{ id: string }[]>`
      UPDATE accounts
      SET balance_cents = balance_cents - ${input.amountCents}
      WHERE id = ${input.fromId}
        AND balance_cents >= ${input.amountCents}
      RETURNING id
    `;

    if (debited.length !== 1) {
      throw new Error("Source account is missing or has insufficient funds");
    }

    const credited = await transaction<{ id: string }[]>`
      UPDATE accounts
      SET balance_cents = balance_cents + ${input.amountCents}
      WHERE id = ${input.toId}
      RETURNING id
    `;

    if (credited.length !== 1) {
      throw new Error("Destination account is missing");
    }
  });
}
```

Values inside `${...}` are sent as parameters by the client. They are not pasted into SQL text. If either update or either explicit check throws, the transaction rolls back both writes.

The database constraint prevents a negative balance. The conditional debit also makes insufficient funds a controlled result. For a high-contention financial system, locking, isolation, idempotency, audit records, and ledger design need deeper treatment than this teaching example.

## 5. Test the boundary

Use a dedicated test database. Seed two accounts before each test and delete the test data afterward. Verify at least:

1. A valid transfer changes both balances by the same amount.
2. Insufficient funds change neither balance.
3. A missing destination rolls back the debit.
4. A zero, negative, fractional, or unsafe amount is rejected before SQL.
5. Repeating a request is not assumed safe. A real mutation needs an idempotency design when clients may retry.

Do not mock the SQL client for transaction tests. A mock cannot prove that PostgreSQL rolls back the first update when the second fails.

## Common mistakes

- Importing the database module into a Client Component.
- Creating a new client for every function call.
- Building SQL by joining strings with user input.
- Testing only the successful transaction.
- Assuming a transaction automatically makes a retried business command idempotent.
- Using production credentials or data in local tests.

## Check your understanding

1. Why is the connection module marked `server-only`?
2. How are interpolated values handled by Postgres.js tagged templates?
3. What causes both updates to roll back?
4. Why is the database check constraint still needed?
5. Why must transaction behavior be tested against a real disposable database?

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 20](../20-external-apis-secrets-timeouts-and-failure-handling/README.md).
