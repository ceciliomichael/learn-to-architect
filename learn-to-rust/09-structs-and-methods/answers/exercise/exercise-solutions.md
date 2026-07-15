# Exercise Solutions: Structs and Methods

```rust
#[derive(Debug)]
struct Product {
    name: String,
    price_cents: u32,
}

impl Product {
    fn new(name: String, price_cents: u32) -> Self {
        Self { name, price_cents }
    }
    fn name(&self) -> &str {
        &self.name
    }
    fn price_cents(&self) -> u32 {
        self.price_cents
    }
    fn set_price(&mut self, price_cents: u32) {
        self.price_cents = price_cents;
    }
    fn into_name(self) -> String {
        self.name
    }
}

fn main() {
    let mut first = Product::new(String::from("Pen"), 125);
    let second = Product::new(String::from("Book"), 1200);
    first.set_price(150);
    println!(
        "{} {} {}",
        first.name(),
        first.price_cents(),
        second.price_cents()
    );
    println!("{}", second.into_name());
}
```

`into_name` consumes `second`; it cannot be used afterward.
