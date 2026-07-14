# Exercise: Describe inventory items

1. Define a `Describe` trait with `name(&self) -> &str`.
2. Give it a default `describe` method that returns `Item: {name}`.
3. Create `Book` and `Tool` structs and implement the trait for both.
4. Write `show<T: Describe>(item: &T)` and call it for both values.
5. Override `describe` for `Tool` so it also includes its category.
