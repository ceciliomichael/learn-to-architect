# Exercise Solutions: JSON and CSV Boundaries

```go
package main

import (
	"encoding/csv"
	"encoding/json"
	"fmt"
	"io"
	"os"
	"strconv"
	"strings"
)

type Product struct {
	Name       string `json:"name"`
	PriceCents int    `json:"price_cents"`
}

func decodeProduct(text string) (Product, error) {
	decoder := json.NewDecoder(io.LimitReader(strings.NewReader(text), 4096))
	decoder.DisallowUnknownFields()
	var product Product
	if err := decoder.Decode(&product); err != nil {
		return Product{}, fmt.Errorf("decode product: %w", err)
	}
	var extra any
	if err := decoder.Decode(&extra); err != io.EOF {
		return Product{}, fmt.Errorf("JSON must contain exactly one value")
	}
	if strings.TrimSpace(product.Name) == "" || product.PriceCents < 0 {
		return Product{}, fmt.Errorf("invalid product fields")
	}
	return product, nil
}

func run() error {
	product, err := decodeProduct(`{"name":"Pen","price_cents":125}`)
	if err != nil {
		return err
	}
	fmt.Println(product)
	_, err = decodeProduct(`{"name":"Pen","price_cents":125} {}`)
	fmt.Println("second value rejected:", err != nil)

	var output strings.Builder
	writer := csv.NewWriter(&output)
	records := [][]string{{"name", "price_cents"}, {"Pen", "125"}, {"Book", "1200"}, {"Pad", "350"}}
	if err := writer.WriteAll(records); err != nil {
		return fmt.Errorf("write CSV: %w", err)
	}
	reader := csv.NewReader(strings.NewReader(output.String()))
	header, err := reader.Read()
	if err != nil {
		return fmt.Errorf("read CSV header: %w", err)
	}
	if len(header) != 2 || header[0] != "name" || header[1] != "price_cents" {
		return fmt.Errorf("unexpected CSV header")
	}
	for {
		record, err := reader.Read()
		if err == io.EOF {
			break
		}
		if err != nil {
			return fmt.Errorf("read CSV record: %w", err)
		}
		if len(record) != 2 {
			return fmt.Errorf("invalid CSV record")
		}
		price, err := strconv.Atoi(record[1])
		if err != nil {
			return fmt.Errorf("parse CSV price: %w", err)
		}
		if price < 0 {
			return fmt.Errorf("CSV price must be nonnegative")
		}
		fmt.Println(record[0], price)
	}
	return nil
}

func main() {
	if err := run(); err != nil {
		fmt.Fprintln(os.Stderr, "data processing failed:", err)
		os.Exit(1)
	}
}
```

The boundary functions return errors rather than panicking on invalid external data. `main` reports the failure once.
