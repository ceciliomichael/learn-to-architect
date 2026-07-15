# Module 31: Dependencies, API Design, and Supply-Chain Safety

## What you will learn

You will add dependencies intentionally, inspect module changes, and design a small public contract that can evolve safely.

Go modules record direct and indirect requirements in `go.mod` and content checksums in `go.sum`. Checksums detect changed downloaded content; they do not prove that a dependency is safe, maintained, correctly licensed, or appropriate.

Use `go get module/path@version` to choose a dependency deliberately. Use `go mod tidy` to align requirements with imports, then review the diff. `go mod verify` checks cached module content. `go list -m -u all` can show available updates, but updates still require release-note review and tests.

Install the official vulnerability scanner separately when your environment approves it:

```text
go install golang.org/x/vuln/cmd/govulncheck@latest
govulncheck ./...
```

Pin tools through a documented team process. The word `latest` is convenient for a manual installation but is not a reproducible CI policy.

Every exported name adds compatibility cost. Prefer focused packages, accept behavior at the consumer boundary, return concrete values when useful, and document errors and concurrency guarantees. Semantic import versioning places version 2 and newer in the module path.

Review transitive dependencies, licenses, source repository, maintainers, release activity, build behavior, and network access. Use the smallest trusted dependency set that solves a real problem.

## Check your understanding

You are ready when you can explain every changed module line and the compatibility promise of every exported name.
