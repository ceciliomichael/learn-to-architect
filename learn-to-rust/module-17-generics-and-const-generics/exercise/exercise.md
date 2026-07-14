# Exercise: Store and inspect pairs

Create a generic `Pair<T>` with `left` and `right` fields.

1. Add a `new` associated function.
2. Add `left()` and `right()` methods that borrow and return each value.
3. Write `array_first<T, const N: usize>` that returns `Option<&T>`.
4. In `main`, use `Pair` with integers and with strings. Test `array_first` with a three-item array.

Do not clone values. The accessor functions should borrow them.
