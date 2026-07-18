# Module 34: Profiling, Optimization, and Releasing Go Programs

## What you will learn

You will collect performance evidence, improve the right bottleneck, and release a verified artifact with known inputs.

Start with correctness tests and a representative workload. Use benchmarks for small operations and `runtime/pprof` or `net/http/pprof` in controlled environments for CPU and heap profiles. Profiles contain function names, paths, and workload details, so protect them as sensitive operational data.

Useful commands include:

```text
go test -bench=. -benchmem ./...
go test -cpuprofile cpu.out -memprofile memory.out ./...
go tool pprof cpu.out
go build -gcflags=-m=2 ./cmd/app
```

Escape analysis output explains compiler decisions but is not a command to force every value onto the stack. Optimize algorithms and allocations only when evidence shows meaningful impact. Keep before-and-after tests and measurements in the same environment.

Release from a clean, reviewed revision. Run formatting checks, tests, race-enabled tests on supported platforms, static analysis, vulnerability checks, and reproducible builds. Record Go version, module graph, source revision, target, build flags, checksums, provenance, and rollback policy.

Use `go version -m artifact` to inspect embedded build information. Strip symbols only when operational debugging and policy allow it. Never inject secrets with linker flags because binary strings can be recovered.

## Check your understanding

You are ready when every optimization has a profile or benchmark and every artifact can be traced to reviewed source and tool inputs.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
