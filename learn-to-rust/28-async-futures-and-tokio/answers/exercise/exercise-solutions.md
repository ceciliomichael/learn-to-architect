# Exercise solution

Add Tokio:

```text
cargo add tokio --features rt-multi-thread,macros,time
```

Use this `src/main.rs`:

```rust
use std::time::Duration;
use tokio::time::{sleep, timeout};

async fn delayed_value(value: u32, millis: u64) -> u32 {
    sleep(Duration::from_millis(millis)).await;
    value
}

#[tokio::main]
async fn main() {
    let work = async {
        let (left, right) = tokio::join!(delayed_value(20, 100), delayed_value(22, 150),);
        left + right
    };

    match timeout(Duration::from_secs(1), work).await {
        Ok(total) => println!("total: {total}"),
        Err(_) => {
            eprintln!("work timed out");
            std::process::exit(1);
        }
    }
}
```

`join!` polls both futures as part of the current task. The outer timeout gives the complete operation a deadline.
