# Exercise Solutions: Module 40

## 1. Trace the invariant

Another crate cannot construct the private tuple field directly.

A successfully constructed Port guarantees the value is nonzero according to the constructor contract.

If the field became public, callers could bypass construction validation.

## 2. Repair a weak API

A minimal design is:

~~~rust
/// Temperature measured in degrees Celsius.
#[derive(Debug, Clone, Copy, PartialEq)]
pub struct Temperature {
    celsius: f64,
}

impl Temperature {
    pub fn from_celsius(celsius: f64) -> Self {
        Self { celsius }
    }

    pub fn celsius(self) -> f64 {
        self.celsius
    }
}
~~~

No extra range validation is added because the requirement did not define one.

## 3. Add executable documentation

One reasonable implementation is:

~~~rust
/// Creates a deliberately simple ASCII-oriented slug.
///
/// This helper trims outer whitespace, lowercases ASCII letters,
/// and replaces ASCII spaces with hyphens.
pub fn slug(input: &str) -> String {
    input.trim().to_ascii_lowercase().replace(' ', "-")
}
~~~

The rustdoc example should verify a normal input such as Hello World.

The important part is documenting the limited contract instead of implying complete international text processing.

## 4. Build a Percentage API

A valid core design is:

~~~rust
#[derive(Debug, Clone, Copy, PartialEq, Eq, PartialOrd, Ord)]
pub struct Percentage(u8);

impl Percentage {
    pub fn new(value: u8) -> Result<Self, String> {
        if value > 100 {
            return Err(String::from("percentage must be between 0 and 100"));
        }

        Ok(Self(value))
    }

    pub fn get(self) -> u8 {
        self.0
    }
}
~~~

A structured error can also be appropriate in a reusable library.

## Compatibility review

1. Changing private storage normally does not break ordinary callers if public behavior remains compatible.
2. Renaming a public constructor is source-breaking for code that calls it.
3. Yes. Users may persist, parse, or script around Display output.
4. Yes. Exhaustive matches must handle every variant.
5. The answer depends on the explicit documented contract. Stable behavior should be deliberate rather than accidental.
