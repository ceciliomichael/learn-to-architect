# Exercise Solutions: Tests with the Testing Package

`price.go`:

```go
package price

import (
	"errors"
	"os"
)

var ErrInvalidValue = errors.New("price and quantity must be nonnegative")

func Subtotal(price, quantity int) (int, error) {
	if price < 0 || quantity < 0 {
		return 0, ErrInvalidValue
	}
	return price * quantity, nil
}

func WriteNote(path, text string) error {
	return os.WriteFile(path, []byte(text), 0o600)
}
```

`price_test.go`:

```go
package price

import (
	"errors"
	"os"
	"path/filepath"
	"testing"
)

func TestSubtotal(t *testing.T) {
	tests := []struct {
		name            string
		price, quantity int
		want            int
		wantErr         bool
	}{
		{name: "ordinary", price: 125, quantity: 3, want: 375},
		{name: "zero", price: 125, quantity: 0, want: 0},
		{name: "invalid", price: 125, quantity: -1, wantErr: true},
	}
	for _, test := range tests {
		t.Run(test.name, func(t *testing.T) {
			got, err := Subtotal(test.price, test.quantity)
			if test.wantErr {
				if !errors.Is(err, ErrInvalidValue) {
					t.Fatalf("error = %v, want ErrInvalidValue", err)
				}
				return
			}
			if err != nil || got != test.want {
				t.Fatalf("Subtotal() = %d, %v; want %d, nil", got, err, test.want)
			}
		})
	}
}

func TestWriteNote(t *testing.T) {
	path := filepath.Join(t.TempDir(), "note.txt")
	if err := WriteNote(path, "Go text"); err != nil {
		t.Fatal(err)
	}
	got, err := os.ReadFile(path)
	if err != nil {
		t.Fatal(err)
	}
	if string(got) != "Go text" {
		t.Fatalf("content = %q", got)
	}
}
```

Run `go test -cover ./...`. Coverage reveals executed statements, while assertions determine whether required behavior was actually checked.
