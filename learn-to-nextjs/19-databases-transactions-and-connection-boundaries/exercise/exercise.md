# Exercise: Implement and Prove an Atomic Transfer

## Goal

Use a real disposable PostgreSQL database to prove that a two-account transfer either completes fully or changes nothing.

## Steps

1. Install `postgres` and configure a disposable `DATABASE_URL`.
2. Create the `accounts` table and its nonnegative-balance constraint.
3. Add `app/lib/database.ts` and `app/lib/transfer.ts` from the lesson.
4. Seed account `checking` with 5,000 cents and account `savings` with 1,000 cents.
5. Transfer 750 cents and verify the balances become 4,250 and 1,750.
6. Attempt to transfer 10,000 cents and verify neither balance changes.
7. Attempt a transfer to a missing account and verify the debit is rolled back.
8. Attempt zero, negative, fractional, and unsafe integer amounts and confirm no query changes data.
9. Explain why parameterized values, a transaction, and a database constraint solve different problems.

## Success check

- Credentials remain in an ignored local environment file.
- Database code cannot enter a client bundle.
- No query is assembled by concatenating input.
- Both successful balances and rollback balances are asserted.
- Tests create and clean up only disposable records.
