# Exercise solution

```rust
use std::rc::Rc;

#[derive(Debug)]
struct CatalogItem {
    name: Rc<String>,
    location: String,
}

fn main() {
    let shared_name = Rc::new(String::from("Safety Guide"));
    let shelf = CatalogItem {
        name: Rc::clone(&shared_name),
        location: String::from("Shelf A"),
    };

    println!("count: {}", Rc::strong_count(&shared_name));
    {
        let archive = CatalogItem {
            name: Rc::clone(&shared_name),
            location: String::from("Archive"),
        };
        println!("{} at {}", archive.name, archive.location);
        println!("count: {}", Rc::strong_count(&shared_name));
    }

    println!("{} at {}", shelf.name, shelf.location);
    println!("count: {}", Rc::strong_count(&shared_name));
}
```

`Arc` makes the reference count safe across threads. Safe mutation still needs an atomic value, a lock, or a design based on messages.
