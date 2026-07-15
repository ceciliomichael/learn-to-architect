# Exercise solution

Use this `src/lib.rs`, replacing `percentage_course` in the examples if your package has another name:

```rust
/// A whole-number percentage from 0 through 100.
#[derive(Debug, PartialEq, Eq)]
pub struct Percentage(u8);

impl Percentage {
    /// Creates a validated percentage.
    ///
    /// # Examples
    ///
    /// ```
    /// use percentage_course::Percentage;
    ///
    /// let value = Percentage::new(75)?;
    /// assert_eq!(value.value(), 75);
    /// # Ok::<(), String>(())
    /// ```
    ///
    /// Values greater than 100 are rejected.
    ///
    /// ```
    /// use percentage_course::Percentage;
    /// assert!(Percentage::new(101).is_err());
    /// ```
    pub fn new(value: u8) -> Result<Self, String> {
        if value <= 100 {
            Ok(Self(value))
        } else {
            Err(String::from("percentage must not exceed 100"))
        }
    }

    /// Returns the validated whole-number value.
    pub fn value(&self) -> u8 {
        self.0
    }
}
```

The private field prevents callers from constructing an invalid value without going through `new`.
