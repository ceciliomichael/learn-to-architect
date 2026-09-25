# Exercises: Module 26

Work locally and explain your choices.

## 1. Trace

Why can writing diagnostics to stdout break another program even if a human sees useful text?

## 2. Repair

Replace direct args[1] indexing with validated parsing or a CLI parser.

## 3. Modify

Add a --verbose flag and a Remove { index: usize } subcommand.

## 4. Build

Create a config resolution function that receives optional CLI value, optional environment value, and a default, then returns the chosen value with a documented precedence.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
