# Module 32: Reflection

## What you will learn

You will inspect runtime types safely, understand addressability and validity, and prefer ordinary typed code when possible.

```go
package main

import (
	"fmt"
	"reflect"
)

func describe(input any) {
	value := reflect.ValueOf(input)
	if !value.IsValid() {
		fmt.Println("nil interface")
		return
	}
	fmt.Println(value.Type(), value.Kind())
}

func main() { describe(42) }
```

`reflect.Type` describes a Go type. `reflect.Value` holds a runtime value. `Kind` is its underlying category such as struct, slice, or pointer. Check `IsValid` before using a zero Value and check `Kind` before kind-specific operations.

Setting requires an addressable, settable value, commonly reached by passing a non-nil pointer and using `Elem`. `CanSet` and conversion checks prevent panics. Reflection bypasses much compile-time clarity and can turn ordinary mistakes into runtime failures.

Struct tags are accessible through reflection but remain metadata. Libraries such as JSON codecs decide their meaning. Do not write a validator that assumes tags alone make external data safe.

Use reflection for infrastructure that genuinely handles unknown types. Prefer interfaces, generics, code generation, or explicit fields for application rules.

## Check your understanding

You are ready when you can check validity, kind, and settable state before a reflective operation.

## Practice and answers

Complete the [exercise](./exercise/exercise.md), then take the [quiz](./quiz/quiz.md). Try both before reading the [exercise solution](./answers/exercise/exercise-solutions.md) or [quiz answers](./answers/quiz/quiz-answers.md).
