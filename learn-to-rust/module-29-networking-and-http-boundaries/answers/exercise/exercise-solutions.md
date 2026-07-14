# Exercise solution

Add dependencies:

```text
cargo add reqwest
cargo add tokio --features rt-multi-thread,macros
```

Use this `src/main.rs`:

```rust
use std::error::Error;
use std::time::Duration;

const MAX_BODY_BYTES: usize = 100_000;

async fn run() -> Result<(), Box<dyn Error>> {
    let client = reqwest::Client::builder()
        .timeout(Duration::from_secs(10))
        .build()?;
    let mut response = client
        .get("https://example.com/")
        .send()
        .await?
        .error_for_status()?;

    let mut size = 0;
    while let Some(chunk) = response.chunk().await? {
        size += chunk.len();
        if size > MAX_BODY_BYTES {
            return Err("response exceeded 100,000 bytes".into());
        }
    }
    println!("received {size} bytes");
    Ok(())
}

#[tokio::main]
async fn main() {
    if let Err(error) = run().await {
        eprintln!("request failed: {error}");
        std::process::exit(1);
    }
}
```

The loop enforces the actual number of bytes received instead of trusting the optional `Content-Length` header.
