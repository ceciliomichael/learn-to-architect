# Module 05: Strings, Bytes, Runes, and Unicode

## What you will learn

You will distinguish UTF-8 text, bytes, and Unicode code points without assuming one byte equals one visible character.

## Go strings contain bytes

```go
package main

import (
	"fmt"
	"unicode/utf8"
)

func main() {
	text := "Go cafe\u0301"
	fmt.Println(text)
	fmt.Println("bytes:", len(text))
	fmt.Println("runes:", utf8.RuneCountInString(text))
}
```

Go source is UTF-8. A string stores an immutable sequence of bytes, and `len` reports bytes. A rune is an alias for `int32` used for one Unicode code point. A visible symbol can contain multiple code points, so rune count is not always human-visible character count.

## Literals and indexing

Double quotes create interpreted strings with escapes such as `\n`. Backticks create raw strings that preserve most characters and line breaks. Single quotes create one rune literal, such as `'G'`.

`text[0]` returns one byte, not a string or guaranteed complete character. Do not slice arbitrary user text by byte positions. Module 07 teaches safe rune iteration, and Module 09 teaches byte and rune slices.

Use `strings` functions for known text operations. Case conversion and comparison can have domain-specific international rules. Do not treat lowercasing as universal identity normalization.

## Check your understanding

You are ready when you can explain why byte length, rune count, and visible character count may differ.
