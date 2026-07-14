# Exercise Solutions: Repeat Work with For and Range

```go
package main

import "fmt"

func main() {
	for number := 1; number <= 10; number++ {
		fmt.Println(number)
	}

	for count := 5; count >= 1; count-- {
		fmt.Println(count)
	}

	total := 0
	for number := 1; number <= 100; number++ {
		total += number
	}
	fmt.Println("total:", total)

	for byteIndex, character := range "Go\u4e16\u754c" {
		fmt.Printf("%d %c\n", byteIndex, character)
	}
}
```

The total is 5050. The Unicode byte indexes are not consecutive after ASCII because each CJK rune uses multiple UTF-8 bytes.
