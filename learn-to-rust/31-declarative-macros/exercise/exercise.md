# Exercises: Module 31

Work locally and explain your choices.

## 1. Trace

Why can a macro accept a variable number of comma-separated expressions in a way a normal Rust function signature cannot?

## 2. Repair

Make a macro pattern accept only literal, pass an identifier, then change the pattern to the narrowest appropriate fragment.

## 3. Modify

Change strings! so zero arguments produce an empty Vec<String> without type-inference ambiguity at the call site you choose.

## 4. Build

Create a simple ensure! macro taking a Boolean expression and error expression, returning early with Err(error) when the condition is false. Compare it with an ordinary helper function and state when the macro is justified.

Finish with cargo fmt, cargo clippy, cargo test when tests exist, and cargo check.
