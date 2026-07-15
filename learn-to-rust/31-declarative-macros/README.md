# Module 31: Declarative Macros

A declarative macro writes Rust code from matched syntax. `println!` and `vec!` are familiar examples. Define one with `macro_rules!`.

```rust
macro_rules! label {
    ($name:expr, $value:expr) => {
        format!("{}: {}", $name, $value)
    };
}

fn main() {
    println!("{}", label!("lessons", 31));
}
```

Fragment specifiers describe accepted syntax. Common ones include `expr` for an expression, `ident` for an identifier, `ty` for a type, and `item` for an item. Repetition uses forms such as `$(...),*`.

Macros are expanded before ordinary type checking. They can accept variable syntax and generate repeated structures, but their errors are often harder for beginners to read. Prefer a function when normal parameters and return values solve the problem.

Rust macros are hygienic: names created inside a macro do not normally collide with names at the call site. Still, evaluate each input expression only once unless repeated evaluation is an explicit and documented part of the macro. Extra evaluation can repeat side effects.

Keep macros small, give invalid uses clear compile errors when possible, and test several valid call forms. Procedural macros are separate compiler plugins and add a larger dependency and review boundary; they are outside this course's implementation scope.

Continue to [Module 32](../32-unsafe-rust-and-safety-contracts/README.md).
