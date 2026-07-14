# Exercises: Dependencies, API Design, and Supply-Chain Safety

1. Inspect `go env GOPROXY GOSUMDB` without changing them.
2. Add one disposable dependency at an explicit version and review `go.mod` and `go.sum`.
3. Run tests, `go mod verify`, and an approved vulnerability scan.
4. Remove the import, run `go mod tidy`, and inspect the diff again.
5. Reduce a broad public interface to the methods one consumer actually needs.
