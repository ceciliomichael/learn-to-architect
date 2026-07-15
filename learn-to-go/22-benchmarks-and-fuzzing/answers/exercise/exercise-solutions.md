# Exercise Solutions: Benchmarks and Fuzz Tests

`reverse.go`:

```go
package text

func Reverse(input string) string {
	runes := []rune(input)
	for left, right := 0, len(runes)-1; left < right; left, right = left+1, right-1 {
		runes[left], runes[right] = runes[right], runes[left]
	}
	return string(runes)
}
```

`reverse_test.go`:

```go
package text

import (
	"testing"
	"unicode/utf8"
)

func FuzzReverseTwice(f *testing.F) {
	for _, seed := range []string{"", "Go", "Go\u4e16\u754c"} {
		f.Add(seed)
	}
	f.Fuzz(func(t *testing.T, input string) {
		if !utf8.ValidString(input) {
			t.Skip()
		}
		if got := Reverse(Reverse(input)); got != input {
			t.Fatalf("double reverse changed %q to %q", input, got)
		}
	})
}

func BenchmarkSliceMembership(b *testing.B) {
	values := make([]int, 10_000)
	for index := range values {
		values[index] = index
	}
	b.ReportAllocs()
	b.ResetTimer()
	for range b.N {
		for _, value := range values {
			if value == 9_999 {
				break
			}
		}
	}
}
```

Run `go test`, `go test -bench=. -benchmem`, and `go test -fuzz=FuzzReverseTwice -fuzztime=10s`. Add a separate map benchmark before comparing the two data structures.
