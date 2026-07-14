# Module 09: Structs and Methods

## What you will learn

You will model named data and control how it is read or changed with methods.

```rust
#[derive(Debug)]
struct Account {
    owner: String,
    balance_cents: i64,
}

impl Account {
    fn new(owner: String) -> Self {
        Self {
            owner,
            balance_cents: 0,
        }
    }

    fn deposit(&mut self, cents: i64) {
        self.balance_cents += cents;
    }
}
```

Named structs explain fields. Tuple structs express small positional wrappers; unit structs carry type identity without fields. Methods live in `impl` blocks. Receivers are `&self`, `&mut self`, or `self` depending on whether they read, mutate, or consume.

Associated functions such as `new` have no receiver and are called with `Account::new`. Constructors are conventions, not special syntax.

Struct update syntax can move owned fields from the source. Derive traits only when their generated behavior matches the domain. Keep fields private when callers should use a smaller, clearer set of operations. Modules 11 and 12 will show constructors that can reject invalid input.

## Check your understanding

You are ready when you can choose a receiver and predict which fields move, borrow, or copy.
