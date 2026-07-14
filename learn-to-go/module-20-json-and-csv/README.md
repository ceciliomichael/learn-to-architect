# Module 20: JSON and CSV Boundaries

## What you will learn

You will decode external data into explicit shapes, reject unexpected content, validate meaning, and stream records when appropriate.

```go
package main

import (
	"encoding/json"
	"fmt"
	"strings"
)

type ProductInput struct {
	Name       string `json:"name"`
	PriceCents int    `json:"price_cents"`
}

func main() {
	decoder := json.NewDecoder(strings.NewReader(`{"name":"Pen","price_cents":125}`))
	decoder.DisallowUnknownFields()
	var input ProductInput
	if err := decoder.Decode(&input); err != nil {
		fmt.Println("invalid JSON")
		return
	}
	if input.Name == "" || input.PriceCents < 0 {
		fmt.Println("invalid product")
		return
	}
	fmt.Println(input)
}
```

Successful decoding proves syntax and requested field conversions, not domain validity. Struct tags map external names; they do not validate. `DisallowUnknownFields` is useful for strict owned request schemas, but can harm compatibility when ignored fields are part of the contract.

Bound request size before decoding. For one JSON value, verify that no second non-whitespace value remains. Avoid decoding arbitrary data into `any` when a known struct is safer.

CSV fields are text. Verify headers, record width, conversions, and row limits. Open CSV files with the platform-safe newline behavior described by Go's reader and writer APIs. Protect spreadsheet exports from formula interpretation when recipients open them in spreadsheet software.

## Check your understanding

You are ready when you can separate decoding, structural policy, domain validation, and trusted use.
