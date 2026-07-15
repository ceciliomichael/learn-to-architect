# Exercise: Sum two halves

1. Create `numbers = vec![1, 2, 3, 4, 5, 6]`.
2. Use `thread::scope` to start two workers that borrow separate halves.
3. Each worker returns its partial sum.
4. Join both workers and print the combined total.
5. Report a worker panic without using `unwrap` or `expect`.
