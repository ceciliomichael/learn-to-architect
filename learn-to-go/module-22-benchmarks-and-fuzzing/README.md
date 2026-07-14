# Module 22: Benchmarks and Fuzz Tests

## What you will learn

You will measure representative work and use generated inputs to discover violated properties.

Benchmarks use `BenchmarkXxx(*testing.B)` and run the operation `b.N` times. Use `b.ReportAllocs`, keep setup out of the measured region with `b.ResetTimer`, and compare results on the same machine and toolchain. One small result does not prove production speed.

Fuzz tests use `FuzzXxx(*testing.F)`. Add seed cases, then state a property that must hold for every generated input.

```go
package text

import (
	"strings"
	"testing"
	"unicode/utf8"
)

func FuzzReverseTwice(f *testing.F) {
	f.Add("Go")
	f.Add("world")
	f.Fuzz(func(t *testing.T, input string) {
		if !utf8.ValidString(input) {
			t.Skip()
		}
		if got := Reverse(Reverse(input)); got != input {
			t.Fatalf("double reverse changed %q to %q", input, got)
		}
	})
}

func BenchmarkNormalize(b *testing.B) {
	b.ReportAllocs()
	for range b.N {
		_ = strings.TrimSpace("  Go Course  ")
	}
}
```

Run ordinary seed coverage with `go test`. Run bounded fuzzing locally with `go test -fuzz=FuzzReverseTwice -fuzztime=10s`. A failing input is saved as a regression seed. Never fuzz production systems or unbounded external targets.

## Check your understanding

You are ready when you can state what is measured, what property is fuzzed, and what environment produced the evidence.
