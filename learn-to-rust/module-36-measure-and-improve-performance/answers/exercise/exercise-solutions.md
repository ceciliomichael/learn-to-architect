# Exercise solution

```rust
use std::time::{Duration, Instant};

fn repeated_add(count: usize) -> String {
    let mut output = String::new();
    for number in 0..count {
        let piece = format!("item-{number}\n");
        output = output + &piece;
    }
    output
}

fn reserved_push(count: usize) -> String {
    let mut output = String::with_capacity(count * 12);
    for number in 0..count {
        output.push_str(&format!("item-{number}\n"));
    }
    output
}

fn measure<F>(runs: usize, work: F) -> Duration
where
    F: Fn() -> String,
{
    let start = Instant::now();
    for _ in 0..runs {
        std::hint::black_box(work());
    }
    start.elapsed()
}

fn main() {
    const COUNT: usize = 10_000;
    const RUNS: usize = 5;
    assert_eq!(repeated_add(COUNT), reserved_push(COUNT));

    println!("repeated add: {:?}", measure(RUNS, || repeated_add(COUNT)));
    println!(
        "reserved push: {:?}",
        measure(RUNS, || reserved_push(COUNT))
    );
    println!("record rustc version, target, operating system, and hardware");
}
```

Run with `cargo run --release` several times. This small timer is educational, not a substitute for a statistical benchmark harness and profiler.
