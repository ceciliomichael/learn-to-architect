# Exercise solution

```rust
struct Pair<T> {
    left: T,
    right: T,
}

impl<T> Pair<T> {
    fn new(left: T, right: T) -> Self {
        Self { left, right }
    }

    fn left(&self) -> &T {
        &self.left
    }

    fn right(&self) -> &T {
        &self.right
    }
}

fn array_first<T, const N: usize>(items: &[T; N]) -> Option<&T> {
    items.first()
}

fn main() {
    let numbers = Pair::new(4, 9);
    let words = Pair::new(String::from("north"), String::from("south"));
    let colors = ["red", "green", "blue"];

    println!("{} {}", numbers.left(), numbers.right());
    println!("{} {}", words.left(), words.right());
    println!("{:?}", array_first(&colors));
}
```

The accessors return references, so the pair keeps ownership. `array_first` accepts arrays of any element type and length.
