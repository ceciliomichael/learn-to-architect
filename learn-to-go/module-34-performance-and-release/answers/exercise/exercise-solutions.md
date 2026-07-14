# Exercise Solutions: Profiling, Optimization, and Releasing Go Programs

Use one package with correctness tests and benchmarks, then run:

```text
gofmt -w .
go test ./...
go test -race ./...
go vet ./...
go test -bench=. -benchmem ./...
go test -run=TestRepresentativeWork -cpuprofile=cpu.out ./internal/work
go tool pprof -top cpu.out
go build -trimpath -o dist/app ./cmd/app
go version -m dist/app
```

In PowerShell, calculate a SHA-256 checksum with:

```text
Get-FileHash -Algorithm SHA256 dist/app
```

On macOS or Linux, use an available SHA-256 tool such as `sha256sum`. Record the exact command and environment.

A valid improvement report includes the unchanged correctness tests, before and after benchmark samples, profile evidence naming the bottleneck, Go version, operating system, CPU, data size, and any readability or memory tradeoff. If evidence does not improve, keep the clearer original code.
