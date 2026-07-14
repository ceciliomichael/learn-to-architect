# Exercise Solutions: Test Rust Code

`src/lib.rs`:

```rust
/// Returns a subtotal for nonnegative inputs.
///
/// ```
/// assert_eq!(rust_practice::subtotal(125, 3), Ok(375));
/// ```
pub fn subtotal(cents: i64, quantity: i64) -> Result<i64, &'static str> {
    if cents < 0 || quantity < 0 {
        Err("values must be nonnegative")
    } else {
        Ok(cents * quantity)
    }
}

#[cfg(test)]
mod tests {
    use super::*;
    #[test]
    fn ordinary() {
        assert_eq!(subtotal(125, 3), Ok(375));
    }
    #[test]
    fn zero() {
        assert_eq!(subtotal(125, 0), Ok(0));
    }
    #[test]
    fn invalid() {
        assert_eq!(subtotal(125, -1), Err("values must be nonnegative"));
    }
}
```

`tests/public_api.rs`:

```rust
#[test]
fn public_subtotal() {
    assert_eq!(rust_practice::subtotal(200, 2), Ok(400));
}
```

Run `cargo test` and `cargo test ordinary`.

The unit tests check an ordinary subtotal, the zero boundary, and invalid input. The integration test uses only the public crate API, while the documentation test proves that the example shown to users still compiles and behaves as written.
