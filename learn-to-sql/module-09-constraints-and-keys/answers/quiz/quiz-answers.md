# Quiz Answers: Protect Data with Constraints and Keys

1. One row or entity uniquely.
2. The referenced parent key must exist, subject to the relationship definition.
3. A missing value can make the check unknown rather than false, so `NOT NULL` separately forbids missing data.
4. No.
5. Enable `PRAGMA foreign_keys = ON` for each connection unless their framework guarantees it.
