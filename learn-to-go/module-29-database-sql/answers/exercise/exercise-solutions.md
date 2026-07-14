# Exercise Solutions: SQL from Go

Create a module and add a reviewed pure-Go SQLite driver:

```text
go mod init example.com/sql-practice
go get modernc.org/sqlite
```

`main.go`:

```go
package main

import (
	"context"
	"database/sql"
	"errors"
	"fmt"
	"os"
	"time"

	_ "modernc.org/sqlite"
)

func listProducts(ctx context.Context, database *sql.DB) (err error) {
	rows, err := database.QueryContext(ctx, "SELECT name, price_cents FROM products ORDER BY name")
	if err != nil {
		return fmt.Errorf("query products: %w", err)
	}
	defer func() {
		if closeErr := rows.Close(); err == nil && closeErr != nil {
			err = fmt.Errorf("close product rows: %w", closeErr)
		}
	}()

	for rows.Next() {
		var name string
		var price int
		if err := rows.Scan(&name, &price); err != nil {
			return fmt.Errorf("scan product: %w", err)
		}
		fmt.Println(name, price)
	}
	if err := rows.Err(); err != nil {
		return fmt.Errorf("iterate products: %w", err)
	}
	return nil
}

func run() (err error) {
	database, err := sql.Open("sqlite", ":memory:")
	if err != nil {
		return fmt.Errorf("open database: %w", err)
	}
	defer func() {
		if closeErr := database.Close(); err == nil && closeErr != nil {
			err = fmt.Errorf("close database: %w", closeErr)
		}
	}()

	ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
	defer cancel()
	if _, err := database.ExecContext(ctx, `CREATE TABLE products (
		product_id INTEGER PRIMARY KEY,
		name TEXT NOT NULL UNIQUE,
		price_cents INTEGER NOT NULL CHECK (price_cents >= 0)
	)`); err != nil {
		return fmt.Errorf("create products table: %w", err)
	}
	tx, err := database.BeginTx(ctx, nil)
	if err != nil {
		return fmt.Errorf("begin product transaction: %w", err)
	}
	defer func() {
		rollbackErr := tx.Rollback()
		if err == nil && rollbackErr != nil && !errors.Is(rollbackErr, sql.ErrTxDone) {
			err = fmt.Errorf("roll back product transaction: %w", rollbackErr)
		}
	}()
	for _, product := range []struct {
		name  string
		price int
	}{{"Pen", 125}, {"Book", 1200}, {"Pad", 350}} {
		if _, err := tx.ExecContext(ctx, "INSERT INTO products(name, price_cents) VALUES (?, ?)", product.name, product.price); err != nil {
			return fmt.Errorf("insert product %q: %w", product.name, err)
		}
	}
	if err := tx.Commit(); err != nil {
		return fmt.Errorf("commit products: %w", err)
	}
	var name string
	var price int
	err = database.QueryRowContext(ctx, "SELECT name, price_cents FROM products WHERE name = ?", "Pad").Scan(&name, &price)
	if errors.Is(err, sql.ErrNoRows) {
		fmt.Println("not found")
	} else if err != nil {
		return fmt.Errorf("query Pad: %w", err)
	} else {
		fmt.Println(name, price)
	}
	if err := listProducts(ctx, database); err != nil {
		return err
	}
	return nil
}

func main() {
	if err := run(); err != nil {
		fmt.Fprintln(os.Stderr, "database exercise failed:", err)
		os.Exit(1)
	}
}
```

Review `go.mod`, `go.sum`, driver maintenance, license, advisories, and supported SQLite behavior before production use.
