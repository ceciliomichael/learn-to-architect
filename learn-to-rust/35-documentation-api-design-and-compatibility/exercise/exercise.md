# Exercise: Document a bounded percentage

Create a library with a `Percentage` type.

1. Keep its `u8` field private.
2. Provide `Percentage::new(value: u8) -> Result<Self, String>` for values from 0 through 100.
3. Provide a `value(&self) -> u8` accessor.
4. Add useful rustdoc with success and error examples.
5. Run `cargo test` and `cargo doc --no-deps`.
