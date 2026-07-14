# Module 05: Functions, Scope, and Tuples

## What you will learn

You will write focused functions, return expression values, and group a small fixed result in a tuple.

```rust
fn area(width: f64, height: f64) -> f64 {
    width * height
}

fn main() {
    println!("{}", area(3.0, 4.0));
}
```

Parameter types and return types are explicit. The final expression returns because it has no semicolon. `return` is useful for an early exit.

Bindings exist only inside their block. Inner blocks may shadow outer names, but excessive shadowing can confuse ownership later.

A tuple groups a fixed number of values with possibly different types:

```rust
fn bounds() -> (i32, i32) {
    (2, 11)
}
```

Destructure with `let (minimum, maximum) = bounds();`. Use a struct once field names would explain positions better. The empty tuple `()` is called unit and represents no meaningful returned value.

Keep calculations separate from printing so tests and callers can reuse results.

## Check your understanding

You are ready when you can distinguish parameter, argument, return expression, scope, tuple, and unit.
