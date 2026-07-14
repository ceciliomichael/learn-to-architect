# Exercise: Build a small number vector

Create `numbers!` with two call forms:

1. `numbers![1, 2, 3]` returns `vec![1, 2, 3]`.
2. `numbers![5; 3]` returns `vec![5, 5, 5]`.
3. Each expression must be evaluated according to ordinary `vec!` behavior.
4. Demonstrate both forms in `main`.
5. Explain why a macro is justified here instead of a function.
