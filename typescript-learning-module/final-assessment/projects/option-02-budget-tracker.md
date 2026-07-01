# Option 02: Typed Budget & Expense Tracker

**Difficulty:** Intermediate
**Primary Concepts:** Discriminated unions, utility types (`Omit`, `Partial`, `Record`), type guards, Result pattern, functional pipelines

---

## Project Brief

You are building the domain layer of a personal finance application. Financial applications cannot afford silent errors or incorrect state calculations  -  a bad calculation or unhandled type could corrupt a user's entire budget history.

Your engine will track accounts, budgets, and transactions across multiple currencies and categories, producing analytics reports and budget warnings using pure TypeScript.

---

## Domain

An **Account** has:
- `id`: string
- `name`: string
- `type`: `"checking" | "savings" | "credit"`
- `currency`: `"USD" | "EUR" | "GBP"`
- `balance`: number (can be negative for credit accounts)

A **Transaction** is a discriminated union of three types:

```typescript
type IncomeTransaction = {
  type: "income";
  id: string;
  accountId: string;
  amount: number;         // Must be > 0
  source: string;
  date: Date;
};

type ExpenseTransaction = {
  type: "expense";
  id: string;
  accountId: string;
  amount: number;         // Must be > 0
  category: "food" | "housing" | "transport" | "entertainment" | "utilities" | "other";
  description: string;
  date: Date;
};

type TransferTransaction = {
  type: "transfer";
  id: string;
  fromAccountId: string;
  toAccountId: string;
  amount: number;         // Must be > 0
  exchangeRate?: number;  // Required if fromAccount currency !== toAccount currency
  date: Date;
};

type Transaction = IncomeTransaction | ExpenseTransaction | TransferTransaction;
```

A **Budget** tracks spending limits per category for a given month:
- `month`: string (format: `"YYYY-MM"`)
- `limits`: `Record<ExpenseTransaction["category"], number>`

---

## The Result Pattern Requirement

You may NOT throw exceptions for business logic failures in this project. Every public method on your service must return a `Result<T>` union:

```typescript
type Result<T> =
  | { success: true; data: T }
  | { success: false; error: string; code: ErrorCode };

type ErrorCode =
  | "INSUFFICIENT_FUNDS"
  | "INVALID_AMOUNT"
  | "ACCOUNT_NOT_FOUND"
  | "CURRENCY_MISMATCH"
  | "BUDGET_EXCEEDED";
```

---

## Core Requirements

Build a `FinanceEngine` class with these methods:

```typescript
createAccount(name: string, type: Account["type"], currency: Account["currency"]): Result<Account>

recordTransaction(input: CreateTransactionInput): Result<Transaction>
// CreateTransactionInput should use utility types to derive from Transaction
// (omitting 'id' and 'date' which the service generates).
//
// Rules:
// - amount <= 0 returns INVALID_AMOUNT
// - expense on checking/savings where balance < amount returns INSUFFICIENT_FUNDS
// - transfer between different currencies without exchangeRate returns CURRENCY_MISMATCH
// - successfully recording a transaction updates account balance(s) automatically.

getAccountBalance(accountId: string): Result<number>

getMonthlyReport(month: string): Result<MonthlyReport>
// MonthlyReport must include:
// - totalIncome: number
// - totalExpenses: number
// - netSavings: number
// - expensesByCategory: Record<string, number>
// - largestExpense: ExpenseTransaction | null

setBudget(month: string, limits: Partial<Record<ExpenseTransaction["category"], number>>): Result<Budget>

checkBudgetWarnings(month: string): Result<BudgetWarning[]>
// Compares actual expenses in that month against the budget limits.
// Returns a warning for any category where spending is >= 80% of limit.
// BudgetWarning: { category: string; spent: number; limit: number; percentUsed: number }
```

---

## File Structure You Must Use

```
src/
├── types/
│   ├── account.ts
│   ├── transaction.ts
│   ├── budget.ts
│   └── result.ts
├── services/
│   ├── accountService.ts
│   ├── transactionService.ts
│   ├── reportService.ts
│   └── engine.ts           -  FinanceEngine facade combining the services
└── index.ts                -  Entry point demonstrating all scenarios
```

---

## What Your Final index.ts Should Demonstrate

1. Create checking and savings accounts in USD.
2. Record income into checking.
3. Record several categorized expenses.
4. Attempt an expense exceeding the balance  -  show the typed error returned.
5. Record a transfer from checking to savings.
6. Set a monthly budget and record enough spending to trigger an 80% warning.
7. Print the monthly report and budget warnings.
