# Question 03 Answer

**Correct answer: B**  -  `...words: string[]`

A rest parameter collects all the extra arguments passed to the function and groups them into a single array. Because the arguments are collected into an array, the type must be written as an array type. `string[]` means "an array of strings," which is exactly what `words` will be inside the function.

**Type of `words` inside the function:**
`string[]`  -  a regular array of strings. You can call `.length` on it, iterate it with `for...of`, use `.map()`, `.filter()`, etc.

The other options are wrong because
- `...words: string`  -  missing the `[]`, this is not valid rest parameter syntax.
- `words: ...string`  -  the `...` must come before the parameter name, not the type.
- `words: Array`  -  missing the type argument; `Array<string>` would work but is just a longer way to write `string[]`.
