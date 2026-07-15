# Module 14: Pointers, Values, and Mutation

## What you will learn

You will distinguish copied values from shared addresses and make mutation visible in function contracts.

```go
package main

import "fmt"

func addOne(number *int) {
	if number == nil {
		return
	}
	(*number)++
}

func main() {
	count := 4
	addOne(&count)
	fmt.Println(count)
}
```

`&count` obtains the address of `count`. `*number` accesses the value at that address. Go automatically dereferences pointers for struct field access, but it does not provide pointer arithmetic.

Passing an ordinary value copies it. Passing a pointer copies an address that can reach the caller's value. Prefer returning a new small value when that is clearer. Use a pointer when mutation, identity, large-copy avoidance backed by measurement, or optional presence is part of the contract.

The zero value of a pointer is nil. Dereferencing nil panics. Decide whether nil is valid, reject it at the boundary when it is not, and document the choice.

Slices and maps already contain descriptors that reach shared storage. A pointer to a slice is rarely necessary merely to change its elements, though it can be used when replacing the caller's slice header is the explicit API.

## Check your understanding

You are ready when you can trace a copy, an address, and the exact value a function may mutate.
