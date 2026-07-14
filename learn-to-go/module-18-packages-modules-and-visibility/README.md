# Module 18: Packages, Modules, and Visibility

## What you will learn

You will split a project by responsibility, create a module, and expose a small intentional API.

Create a local project:

```text
go mod init example.com/course/shop
```

```text
shop/
|-- go.mod
|-- cmd/shop/main.go
`-- price/price.go
```

`price/price.go`:

```go
package price

func Subtotal(cents, quantity int) int { return cents * quantity }
```

`cmd/shop/main.go` imports `example.com/course/shop/price`. A module is the versioned collection rooted at `go.mod`. A package is the source files compiled together in one directory.

Names beginning with an uppercase Unicode letter are exported from a package. Export only supported contracts. Keep helpers lowercase. Package names should be short and describe what they provide without stuttering in uses such as `price.Subtotal`.

Import cycles are rejected. Move shared foundations lower, pass behavior through a small interface, or redesign responsibilities instead of hiding the cycle.

The `internal` directory prevents imports from outside its permitted parent tree. `init` runs automatically and can hide order-dependent work, so prefer explicit construction and startup validation.

Run `go mod tidy` after imports change. Review resulting dependency changes rather than treating the command as approval.

## Check your understanding

You are ready when you can distinguish repository, module, package, file, and exported identifier.
