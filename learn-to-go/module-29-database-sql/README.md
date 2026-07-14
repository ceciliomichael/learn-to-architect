# Module 29: SQL from Go

## What you will learn

You will use `database/sql` with a reviewed driver, bind every external value, close rows, and keep transactions bounded.

`database/sql` defines a common API and manages a connection pool. A driver supplies database-specific communication. `*sql.DB` is a long-lived pool handle, not one connection, and should normally be reused.

```go
row := database.QueryRowContext(
	ctx,
	"SELECT product_id, name FROM products WHERE product_id = ?",
	productID,
)
if err := row.Scan(&product.ID, &product.Name); err != nil {
	return Product{}, err
}
```

Placeholders bind values only. Never build SQL syntax with user text. Placeholder styles differ by database. Keep identifiers and sort choices in a fixed server-side allowlist.

Use `QueryRowContext` for one row and inspect `sql.ErrNoRows`. For multiple rows, defer `rows.Close`, scan each row, and check `rows.Err` afterward. Use `sql.NullString` or nullable pointers when database null has domain meaning.

Begin a transaction, defer rollback as a safe no-op after commit, perform all operations through `*sql.Tx`, then commit. Keep transactions short and use context deadlines. Configure pool sizes from database capacity and measurements.

## Check your understanding

You are ready when you can trace a bound value, row cleanup, transaction ownership, and context through one database operation.
