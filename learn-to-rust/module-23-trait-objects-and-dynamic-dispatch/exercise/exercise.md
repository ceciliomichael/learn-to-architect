# Exercise: Format different notices

1. Define a `Notice` trait with `format(&self) -> String`.
2. Create `EmailNotice` and `ConsoleNotice` structs with different fields.
3. Implement `Notice` for each.
4. Store one of each in `Vec<Box<dyn Notice>>`.
5. Iterate over the vector and print every formatted notice.
