# Exercise Solutions: Enums, Match, and Patterns

```rust
#[derive(Debug)]
enum OrderState {
    Draft,
    Paid { receipt: String },
    Cancelled { reason: String },
}

fn label(state: &OrderState) -> String {
    match state {
        OrderState::Draft => String::from("draft"),
        OrderState::Paid { receipt } => format!("paid: {receipt}"),
        OrderState::Cancelled { reason } => format!("cancelled: {reason}"),
    }
}

fn main() {
    let state = OrderState::Paid {
        receipt: String::from("R-1"),
    };
    println!("{}", label(&state));
    if let OrderState::Paid { receipt } = &state {
        println!("{receipt}");
    }
    let _draft = OrderState::Draft;
    let _cancelled = OrderState::Cancelled {
        reason: String::from("duplicate"),
    };
}
```

The enum permits only one state at a time.
