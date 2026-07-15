# Exercise Solutions: Reflection

```go
package main

import (
	"fmt"
	"reflect"
)

type Product struct {
	Name       string `json:"name"`
	PriceCents int    `json:"price_cents"`
}

func inspect(input any) {
	value := reflect.ValueOf(input)
	if !value.IsValid() {
		fmt.Println("invalid value")
		return
	}
	fmt.Println(value.Type(), value.Kind())
}

func main() {
	inspect(7)
	inspect("Go")
	inspect([]int{1, 2})
	inspect(nil)

	product := Product{Name: "Pen", PriceCents: 125}
	productType := reflect.TypeOf(product)
	for index := 0; index < productType.NumField(); index++ {
		field := productType.Field(index)
		fmt.Println(field.Name, field.Tag.Get("json"))
	}

	value := reflect.ValueOf(&product)
	if value.Kind() == reflect.Pointer && !value.IsNil() {
		price := value.Elem().FieldByName("PriceCents")
		if price.IsValid() && price.CanSet() && price.Kind() == reflect.Int {
			price.SetInt(150)
		}
	}
	fmt.Println(product)
}
```

The field update checks every runtime assumption. Ordinary `product.PriceCents = 150` remains clearer when the concrete type is already known.
