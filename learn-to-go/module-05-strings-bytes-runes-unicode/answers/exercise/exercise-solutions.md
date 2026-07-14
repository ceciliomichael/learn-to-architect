# Exercise Solutions: Strings, Bytes, Runes, and Unicode

```go
package main

import (
	"fmt"
	"unicode/utf8"
)

func main() {
	fmt.Println("first\nsecond")
	fmt.Println(`first
second`)

	plain := "Go"
	world := "Go\u4e16\u754c"
	fmt.Println(len(plain), utf8.RuneCountInString(plain))
	fmt.Println(len(world), utf8.RuneCountInString(world))

	letter := 'G'
	fmt.Printf("%d %q\n", letter, letter)
}
```

`Go` uses 2 bytes and 2 runes. `Go\u4e16\u754c` uses 8 UTF-8 bytes and 4 runes. A byte index can land inside a multi-byte encoding, so text boundaries must be chosen deliberately.
