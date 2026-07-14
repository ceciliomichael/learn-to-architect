# Exercise solution

```rust
use std::thread;

fn main() {
    let numbers = vec![1, 2, 3, 4, 5, 6];
    let result = thread::scope(|scope| {
        let left = scope.spawn(|| numbers[..3].iter().sum::<i32>());
        let right = scope.spawn(|| numbers[3..].iter().sum::<i32>());

        let left_total = left.join().map_err(|_| "left worker panicked")?;
        let right_total = right.join().map_err(|_| "right worker panicked")?;
        Ok::<i32, &str>(left_total + right_total)
    });

    match result {
        Ok(total) => println!("total: {total}"),
        Err(error) => {
            eprintln!("{error}");
            std::process::exit(1);
        }
    }
}
```

Both workers borrow `numbers`, and the scope ensures both finish before that vector can be dropped.
