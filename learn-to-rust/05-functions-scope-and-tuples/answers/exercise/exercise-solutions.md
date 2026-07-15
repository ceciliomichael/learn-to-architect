# Exercise Solutions: Functions, Scope, and Tuples

```rust
fn area(width: f64, height: f64) -> f64 {
    width * height
}

fn subtotal(price_cents: i32, quantity: i32) -> (i32, bool) {
    if price_cents < 0 || quantity < 0 {
        return (0, false);
    }
    (price_cents * quantity, true)
}

fn bounds() -> (i32, i32) {
    (2, 11)
}

fn main() {
    println!("area: {}", area(3.0, 4.0));
    println!("subtotal: {:?}", subtotal(125, 3));
    let (minimum, maximum) = bounds();
    println!("{minimum} {maximum}");

    {
        let temporary = "inside";
        println!("{temporary}");
    }
}
```

Attempting to print `temporary` after its block fails because the binding is out of scope.
