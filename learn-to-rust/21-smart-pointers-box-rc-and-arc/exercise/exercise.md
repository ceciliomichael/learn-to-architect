# Exercise: Share one catalog label

1. Create a `CatalogItem` struct with `name: Rc<String>` and `location: String`.
2. Create one `Rc<String>` label.
3. Build two items that clone the `Rc` but use different locations.
4. Print both items and `Rc::strong_count` before and after an inner scope.
5. Explain why changing `Rc` to `Arc` alone would not make shared mutation safe.
