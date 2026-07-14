# Exercise Solutions: Vectors and Iteration

```rust
fn main() {
    let mut tasks = vec![String::from("read")];
    tasks.push(String::from("practice"));
    if let Some(task) = tasks.get_mut(0) {
        task.push_str(" lesson");
    }
    println!("{:?} {:?}", tasks.get(1), tasks.get(99));
    for task in &tasks {
        println!("{task}");
    }

    let mut values = vec![-2, 1, 3];
    for value in &mut values {
        *value *= 2;
    }
    values.retain(|value| *value > 0);
    println!("{values:?}");
    println!("popped: {:?}", tasks.pop());
}
```

The lookup at index 99 returns `None` instead of panicking. The first loop borrows each task, so `pop` can still modify the vector later. The second loop uses mutable references to change values in place. `retain` then removes values that do not satisfy its condition.
