# Exercise solution

Root `Cargo.toml`:

```toml
[workspace]
members = ["app", "core"]
resolver = "3"
```

`core/Cargo.toml`:

```toml
[package]
name = "course-core"
version = "0.1.0"
edition = "2024"

[features]
default = []
friendly = []
```

`core/src/lib.rs`:

```rust
#[cfg(feature = "friendly")]
pub fn greeting() -> &'static str {
    "Welcome, learner!"
}

#[cfg(not(feature = "friendly"))]
pub fn greeting() -> &'static str {
    "Welcome"
}
```

`app/Cargo.toml`:

```toml
[package]
name = "course-app"
version = "0.1.0"
edition = "2024"

[dependencies]
course-core = { path = "../core" }
```

`app/src/main.rs`:

```rust
fn main() {
    println!("{}", course_core::greeting());
}
```

Run the default form with `cargo run -p course-app`. To enable the dependency feature, change the app dependency to `{ path = "../core", features = ["friendly"] }` and run it again.
