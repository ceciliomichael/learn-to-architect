# Exercise Solutions: Dependencies, API Design, and Supply-Chain Safety

Use a disposable module:

```text
go mod init example.com/dependency-practice
go env GOPROXY GOSUMDB
go get rsc.io/quote@v1.5.2
go mod verify
go test ./...
```

After inspecting source, license, maintenance, advisories, module files, and the diff, remove the import and run:

```text
go mod tidy
go mod verify
go test ./...
```

A consumer that only writes does not need a broad storage interface:

```go
package report

type Saver interface {
	Save(text string) error
}

func Create(saver Saver, text string) error {
	return saver.Save(text)
}
```

The consumer owns this one-method contract. It does not require unrelated delete, list, transaction, or administration methods.
